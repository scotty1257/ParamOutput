<script lang="ts">
    import ParamBar from "../components/param_bar.svelte";
    import FileInput from "../components/file_input.svelte";
    import { Label, FormText, Input, Form, FormGroup,  ModalFooter, ModalHeader, ModalBody, Modal, ButtonToolbar, Button, ButtonGroup, Col, Row, Container, Icon } from 'sveltestrap';

    let files: any;
    let open = false;
    let fullscreen = true;
    const toggle = () => {
        open = !open;
    };
    let size = 'xl';
    let N_Param = 0;
    let exportXMLstring = "";
    let Params = [
        { 
            name: "", 
            type: "", 
            default_value: "",
            empty: true, 
            number: N_Param, 
            checked: false
        },
    ];

    
    function AddParamToList() {
        ++N_Param;
        Params = Params.concat({ 
            name: "", 
            type: "", 
            default_value: "",
            empty: true, 
            number: N_Param, 
            checked: false
        });
        console.log("Param Added")
    }
    
    function RemoveParamFromList() {
        --N_Param;
        Params = Params.filter(t => !t.checked);
    }
    
    function ExportParams() {
        exportXMLstring = "";
        exportXMLstring += "<?xml version=\"1.0\"?>\n" + 
                            "<Packet xmlns:xsi=\"http://www.w3.org/2001/XMLSchema-instance\" " +
                            "xmlns=\"http://www.solidworks.com\" " + 
                            "xsi:schemaLocation=\"http://www.solidworks.com\" " +
                            "SWXUiPacket.xsd\">\n";

        for (let i = 0; i < Params.length; i++) {
            exportXMLstring += "\t<Parameter Name=" +"\"" + Params[i].name +"\"" +
                               " Type=\"" + Params[i].type + "\"" +
                               " DefaultValue=" + "\"" + Params[i].default_value + "\">\n";
        }

        exportXMLstring += "</packet>";

        toggle();
    }

    function copyXML() {
        navigator.clipboard.writeText(exportXMLstring);

    }

    function importXMLFile() {
        console.log(files[0]);
    }
    
    $: ParamList = Params;
</script>

<div class="page-body">
    <div class="header">
        <h1 class="h1">Parameter and Packet File Import/Export Tool</h1>
    </div>

    <Modal style="white-space: pre;" isOpen={open} toggle={toggle} size={size} {fullscreen} scrollable>
        <ModalHeader {toggle}>XML Output</ModalHeader>
        <ModalBody>
            {exportXMLstring}
            <!-- {exportXMLstring} -->
            <p id="xmlModalP"></p>
        </ModalBody>
        <ModalFooter>
            <Button color="primary" on:click={copyXML}>Copy XML</Button>
            <Button color="secondary" on:click={toggle}>Close</Button>
        </ModalFooter>
    </Modal>
    <Container>
        <FileInput bind:files={files}/>
        {#each Params as Param}
        <div>
            <!-- <input type=checkbox bind:checked={Param.checked}> -->
            <ParamBar 
                bind:checkedParam={Param.checked} 
                bind:ParamName={Param.name} 
                bind:ParamType={Param.type} 
                bind:ParamDefaultValue={Param.default_value}
            />
            <p></p>
        </div>
        {/each}

        <ButtonGroup>
            <Button class="toolbar-button" on:click={AddParamToList}>Add Parameter</Button>
            <Button class="toolbar-button" on:click={RemoveParamFromList}>Remove Selected</Button>
            <Button class="toolbar-button" on:click={ExportParams}>Export XML</Button>
            <Button class="toolbar-button" on:click={importXMLFile}>Import XML</Button>
        </ButtonGroup>
    </Container>
</div>


<style>
    .header {
        margin: auto;
        align-items: center;
        width: 58%;
        border-bottom: 2px solid darkgrey;
        margin-bottom: 20px;
        margin-top: 10px;
    }
    .page-body {
        background-color: lightcyan;
    }
    .h1 {
        @import url('https://fonts.googleapis.com/css2?family=Source+Code+Pro&display=swap');
        text-align: center;
        color: navy;
        margin-bottom: 20px;
        font-family:system-ui, -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, 'Open Sans', 'Helvetica Neue', sans-serif;
        }
    /* .toolbar-button {
        margin: 5px;
    }
    #add-param-button {
        color: navy;
        border: none;
        background-color: aqua;
    }
    button {
        background: none;
        color: inherit;
        border: none;
        padding: 0;
        font: inherit;
        cursor: pointer;
        outline: 0;
    }
    button:focus {
        outline: none;
    } */
</style>