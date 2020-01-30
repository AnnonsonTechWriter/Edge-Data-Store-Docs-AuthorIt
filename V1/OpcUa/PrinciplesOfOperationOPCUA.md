---
uid: PrinciplesOfOperationOPCUA.md
---

# Principles of operation

This topic provides an operational overview of the OPC UA EDS adapter, focusing on streams creation and error handling.

## Adapter configuration

In order for the OPC UA EDS adapter to start data collection, you need to configure the adapter by defining the following:

- Data source: Provide the data source from which the adapter should collect data.
- Data selection: Perform selection of OPC UA items to which the adapter should subscribe for data.
- Logging: Set up the logging attributes to manage the adapter logging behavior.

For more information, see [OPC UA data source configuration](xref:OPCUADataSourceConfiguration) and [OPC UA data selection configuration](xref:OPCUADataSelectionConfiguration). 

## Connection

The OPC UA EDS adapter uses the binary opc.tcp protocol to communicate with the OPC UA servers. A secured connection is enabled by default where the X.509-type client and server certificates are exchanged and verified and the connection between the OPC UA EDS adapter and the configured OPC UA server is established.

## Stream creation

The OPC UA EDS adapter creates types upon receiving the value update for a stream. One stream is created in Edge Data Store for every selected OPC UA item in the data selection configuration.

## Data collection

The OPC UA EDS adapter collects time-series data from selected OPC UA dynamic variables through OPC UA subscriptions (unsolicited reads). The adapter supports the Data Access (DA) part of OPC UA specification.

## Streams by OPC UA EDS adapter

The OPC UA EDS adapter creates a stream with two properties per selected OPC UA item. The properties are described in the following table:

| Property name | Data type | Description |
|---------------|-----------|-------------|
| Timestamp     | DateTime  | Timestamp of the given OPC UA item value update. |
| Value         | Based on type of incoming OPC UA value | Value of the given OPC UA item update. |

Stream ID is a unique identifier for each stream created by the adapter for a given OPC UA item. If the Custom Stream ID is specified for the OPC UA item in data selection configuration, the OPC UA EDS adapter uses that as a stream ID for the stream. Otherwise, the adapter constructs the stream ID using the following format constructed from the OPC UA item node ID:

```
<Adapter Component ID>.<Namespace>.<Identifier>
```

**Note:** The naming convention is affected by StreamIdPrefix and ApplyPrefixToStreamID settings in data source configuration. For more information, see [OPC UA data source configuration](xref:OPCUADataSourceConfiguration).
