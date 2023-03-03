<script>
    import { Styles } from 'sveltestrap';
    import {Input, InputGroup, Row, Col, Icon, Container, Form, FormGroup, FormText, Label } from 'sveltestrap';
    //export let FileName = "";

    /**
	 * @type {any}
	 */
    export let files;
</script>

<div class="custom-file file-input-comp">
    <input 
    type="file" 
    class="custom-file-input" 
    bind:files 
    required>
    {#if files}
        <label class="custom-file-label" for="customInput">{files[0].name}</label>
    {:else}
        <label class="custom-file-label" for="customInput">Choose XML file...</label>
    {/if}
</div>


<style>
   .file-input-comp {
    margin-bottom: 15px;
   }

</style>

