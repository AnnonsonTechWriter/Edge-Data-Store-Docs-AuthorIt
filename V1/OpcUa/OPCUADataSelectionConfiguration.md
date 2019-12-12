---
uid: OPCUADataSelectionConfiguration
---

# Data selection configuration

In addition to the data source configuration, you need to provide a data selection configuration to specify the data you want the OPC UA EDS adapter to collect from the data sources.

## Configure OPC UA data selection

> **Note:** You cannot modify OPC UA data selection configurations manually. You must use the REST endpoints to add or edit the configuration.

Complete the following to configure OPC UA data selection:

1. Using any text editor, create a file that contains an OPC UA data selection in JSON form.
    - For content structure, see [OPC UA data selection example](#opc-ua-data-selection-example).
    - For a table of all available parameters, see [Parameters for OPC UA data selection](#parameters-for-opc-ua-data-selection).
2. Save the file as _DataSelection.config.json_.
3. Use any [tool](xref:managementTools) capable of making HTTP requests to execute a POST command with the contents of that file to the following endpoint: `http://localhost:5590/api/v1/configuration/<EDS adapterId>/DataSelection/`

Example using cURL (run this command from the same directory where the file is located):

```bash
curl -v -d "@DataSelection.config.json" -H "Content-Type: application/json" "http://localhost:5590/api/v1/configuration/<EDS adapterId>/DataSelection"
```

## OPC UA data selection schema

The following table defines the basic behavior of the _OpcUa_DataSelection_schema.json_ file.

| Abstract            | Extensible | Status       | Identifiable | Custom properties | Additional properties |
| ------------------- | ---------- | ------------ | ------------ | ----------------- | --------------------- |
| Can be instantiated | Yes        | Experimental | No           | Forbidden         | Forbidden             |

## Parameters for OPC UA data selection

| Parameter     | Required | Type | Nullable | Description |
|---------------|----------|------|----------|-------------|
| **Selected** | Optional | `boolean` | No | This field is used to select or clear a measurement. To select an item, set to true. To remove an item, leave the field empty or set to false.  If not configured, the default value is false.|
| **Name**      | Optional | `string` | Yes |The optional friendly name of the data item collected from the data source. If not configured, the default value will be the stream id. |
| **NodeId**    | Required | `string` | Yes | The NodeId of the variable. |
| **StreamID** | Optional | `string` | Yes | The custom stream ID that will be used to create the streams. If not specified, the OPC UA EDS adapter will generate a default stream ID based on the measurement configuration. A properly configured custom stream ID follows these rules:<br><br>Is not case-sensitive.<br>Can contain spaces.<br>Cannot start with two underscores ("__").<br>Can contain a maximum of 260 characters.<br>Cannot use the following characters: / : ? # [ ] @ ! $ & ' ( ) \ * + , ; = % < > &#124;<br>Cannot start or end with a period.<br>Cannot contain consecutive periods.<br>Cannot consist of only periods.

## OPC UA data selection example

The following is an example of valid OPC UA Data Selection configuration:

```json
[
 {
    "Selected": true,
    "Name": "Random1",
    "NodeId": "ns=5;s=Random1",
    "StreamId": "CustomStreamName"
  },
  {
    "Selected": false,
    "Name": "Sawtooth1",
    "NodeId": "ns=5;s=Sawtooth1",
    "StreamId": null
  },
  {
    "Selected": true,
    "Name": "Sinusoid1",
    "NodeId": "ns=5;s=Sinusoid1",
    "StreamId": null
  }
]
```
