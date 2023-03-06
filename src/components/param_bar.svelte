<script>
    import { Styles } from 'sveltestrap';
    import { InputGroup, Row, Col, Icon, Container, Form, FormGroup, FormText, Input, Label } from 'sveltestrap';

    export let ParamName = "";
    export let ParamType = "";
    export let ParamDefaultValue = "";

    export let checkedParam = false;
    export let param_number = 0;
</script>

<!-- Name, Type, Default Value -->
<div class="container">
    <Container >
        <Form>
            <FormGroup floating>
                    <p class="number-p"><b>Parameter {param_number} - XML</b></p>
                    <Row style="margin-top: 15px;">
                        <input type=checkbox class="checkbox-radio" bind:checked={checkedParam}>
                        <Col>
                            <Input
                                type="text"
                                name="Name"
                                id="param_name"
                                placeholder="Parameter Name"
                                bind:value={ParamName}
                            />
                        </Col>
                        <Col>
                            <Input
                                type="text"
                                name="Type"
                                id="param_type"
                                placeholder="Parameter Type"
                                bind:value={ParamType}
                            />
                        </Col>
                        <Col>
                            <Input
                                type="text"
                                name="DefaultValue"
                                id="param_default_value"
                                placeholder="Parameter Default Value"
                                bind:value={ParamDefaultValue}
                            />
                        </Col>
                    </Row>
            </FormGroup>
        </Form>
    </Container>
</div>


<style>
    .container {
        margin-bottom: 10px;
        border: 2px solid navy;
        border-radius: 5px;
        padding: 10px;
        background-color: #4ebeef
    }
    input[type=checkbox]{
        transform:scale(1.5);
    }
    .number-p {
        color: #434343
    }
</style>