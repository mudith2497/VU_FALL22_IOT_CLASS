# Data Formats for Transferring Resource Information

## Four data formats are defined by the LWM2M Enabler in this section. The LWM2M Server MUST support all data formats. The plain text and opaque formats MUST be supported by the LWM2M Client. The LWM2M Client MUST support the TLV data format for Object Instance or multiple-instance Resource requests.

The Object specification defines the data format that a Resource supports, either plain text or opaque for singular Resources or TLV for multiple instance Resources.

In addition to the data formats defined in the Object specification, a LWM2M Client MAY choose to support the JSON format for Object Instance or multiple instance Resource requests.

# Plain Text
The plain text format is used for ”Read” and “Write” operations on singular Resources where the value of the Resource is simply represented as an UTF-8 encoded string. This string can contain a character sequence, integer number, decimal number or any other sequence of valid UTF-8 characters as per Appendix A.

For example a request to the example client’s Device Object Instance, Manufacturer Resource would return the following plain text payload:

Req: GET /3/0/0

Res: 2.05 Content

Open Mobile Alliance

This data format has a Media Type of application/vnd.oma.lwm2m+text

# Opaque
The opaque format is used for “Read” and “Write” operations on singular Resources where the value of the Resource is an opaque sequence of binary octets. This data format is used for binary Resources such as firmware images or application specific binary formats.

This data format has a Media Type of application/vnd.oma.lwm2m+opaque

# TLV
For requests to Object Instance or Resource which supports multiple instances (Resource Instance), the binary TLV (Type-Length-Value) format is used to represent an array of values or a singular value using a compact binary representation, which is easy to process on simple embedded devices. The format has a minimum overhead per value of just 2 bytes and a maximum overhead of 5 bytes depending on the type of Identifier and length of the value. The maximum size of an Object Instance or Resource in this format is 16.7 MB. The format is self-describing, thus a parser can skip TLVs for which the Resource is not known.

This data format has a Media Type of application/vnd.oma.lwm2m+tlv

The format is an array of the following byte sequence, where each array entry represents an Object Instance, Resource, or Resource Instance:

Field	Format and Length	Description
Type	8-bits masked field:	Bits 7-6: Indicates the type of Identifier.
Bit 5: Indicates the Length of the Identifier.
Bit 4-3: Indicates the type of Length.
Bits 2-0: A 3-bit unsigned integer indicating the Length of the Value.
Identifier	8-bit or 16-bit unsigned integer as indicated by the Type field.	The Object Instance, Resource, or Resource Instance ID as indicated by the Type field.
Length	0-24-bit unsigned integer as indicated by the Type field.	The Length of the following field in bytes.
Value	Sequence of bytes of Length	Value of the tag. The format of the value depends on the Resource’s data type (See Appendix A).
Table 16: TLV format and description

Each TLV entry starts with a Type byte that indicates if the TLV contains an Object Instance, a Resource, multiple Resources, or a Resource Instance. Object Instance and Resource with Resource Instance TLVs contains other TLVs in their value. The hierarchy is as follows and may be up to 3 levels deep. The Object Instance TLV is only required if multiple Object Instances are returned in a request.

Object Instance TLV, which contains
Resource TLVs or
multiple Resource TLVs, which contains
Resource Instance TLVs
The following figure illustrates the possible nesting of Object Instance, Resource, multiple Resources, and Resource Instance TLVs. One or several Resource TLVs, and/or one or several multiple Resource TLVs MAY be nested in an Object Instance TLV. A multiple Resource TLV contains one or several Resource Instance TLVs.



Single Object Instance Request Example
In this example, a request for the Device Object Instance of the LWM2M example client is made (GET /3/0). The client responds with a TLV payload including all of the readable Resources. This TLV payload would have the following format. The total payload size with the TLV encoding is 121 bytes.

TLV	Type Byte	ID Byte(s)	Length Byte(s)	Value	Total Bytes
Manufacturer Resource	0b11 0 01 000	0x00	0x14 (20 bytes)	Open Mobile Alliance [String]	23
Model Number	0b11 0 01 000	0x01	0x16 (22 bytes)	“Lightweight M2M Client” [String]	25
Serial Number	0b11 0 01 000	0x02	0x09 (9 bytes)	“345000123” [String]	12
Firmware Version	0b11 0 00 011	0x03	(3 bytes)	“1.0” [String]	5
Available Power Sources	0b10 0 00 110	0x06	(6 byte)	The next two rows	2
Available Power Sources[0]	0b01 0 00 001	0x00	(1 byte)	0X01 [8-bit Integer]	3
Available Power Sources[1]	0b01 0 00 001	0x01	(1 byte)	0X05 [8-bit Integer]	3
Power Source Voltage	0b10 0 01 000	0x07	0x08 (8 bytes)	The next two rows	3
Power Source Voltage[0]	0b01 0 00 010	0x00	(2 bytes)	0X0ED8 [16-bit Integer]	4
Power Source Voltage[1]	0b01 0 00 010	0x01	(2 bytes)	0X1388 [16-bit Integer]	4
Power Source Current	0b10 0 00 111	0x08	(7 bytes)	The next two rows	2
Power Source Current[0]	0b01 0 00 001	0x00	(1 byte)	0X7D [8-bit Integer]	3
Power Source Current[1]	0b01 0 00 010	0x01	(2 bytes)	0X0384 [16-bit Integer]	4
Battery Level	0b11 0 00 001	0x09	(1 byte)	0x64 [8-bit Integer]	3
Memory Free	0b11 0 00 001	0x0A	(1 byte)	0x0F [8-bit Integer]	3
Error Code	0b10 0 00 011	0x0B	(3 byte)	The next row	2
Error Code[0]	0b01 0 00 001	0x00	(1 byte)	0x00 [8-bit Integer]	3
Current Time	0b11 0 00 100	0x0D	(4 byte)	0x5182428F [32-bit Integer]	6
Time Zone	0b11 0 00 110	0x0E	(6 byte)	“+02:00” [String]	8
Supported Binding and Modes	0b11 0 00 001	0x0F	(1byte)	“U” [String]	3
Total	121
Multiple Object Instance Request Example
In this example, a request for both the Access Control Objects of the LWM2M example client is made (GET /2). The client responds with a TLV payload including both Object Instances (0 and 1) and their Resources. This TLV payload would have the following format. The total payload size with the TLV encoding is 32 bytes.

TLV	Type Byte	ID Byte(s)	Length Byte(s)	Value	Total Bytes
Access Control Object Instance 0	0b00 0 01 000	0x00	(17 bytes)	The next 5 rows	2
Object ID	0b11 0 00 001	0x00	(1 byte)	0x03 [8-bit Integer]	3
ACL	0b10 0 00 110	0x02	(6 bytes)	The next 2 rows	2
ACL [1]	0b01 0 00 001	0x01	(1 byte)	0b11 10 0000	3
ACL [2]	0b01 0 00 001	0x02	(1 byte)	0b10 00 0000	3
Access Control Owner	0b11 0 00 001	0x03	(1 byte)	0x01 [8-bit Integer]	3
Access Control Object Instance 1	0b00 0 01 000	0x01	(17 bytes)	The next 5 rows	2
Object ID	0b11 0 00 001	0x00	(1 byte)	0x04 [8-bit Integer]	3
ACL	0b10 0 00 001	0x02	(6 bytes)	The next 2 rows	2
ACL [1]	0b01 0 00 001	0x01	(1 byte)	0b10 00 0000	3
ACL [2]	0b01 0 00 001	0x02	(1 byte)	0b10 00 0000	3
Access Control Owner	0b11 0 00 001	0x03	(1 byte)	0x01 [8-bit Integer]	3
Total	32



# JSON

LWM2M Clients supporting the JSON format MUST use the format defined in this section for responses with multiple ressource values. They MAY use the format defined in this section for responses with single value.

The format MUST comply to [SENML] JSON representation and MUST support for all attributes defined in Table 17.

Each entry of the JSON format is a Resource Instance, where the name is the URI path relative to the request URI.

The JSON is useful for returning multi-level Resources from the Resource tree. For example when requesting all Instances of an Object with all Resources, and Resource Instances within a LWM2M Client in the same response.

The JSON format also includes optional time fields, which allows for multiple versions of representations to be sent in the same payload. The time fields MUST only be used when sending notifications. Historical version of notifications are typically generated when “Notification Storing When Disabled or Offline” ressource of LWM2M Server Object is set to true (see Appendix D.2) and when the Device comes on line after having been disabled for a period of time.

This JSON data format has a Media Type of application/vnd.oma.lwm2m+json

Field	JSON Variable	Mandatory?	Description
Resource Array	e	Yes	The Resource list as JSON value array per [SENML].
Name	n	Yes	The Name of the resource is the path of the Resource relative to the request URI.
Time	t	No	The time of the representation relative to the Base Current Time in seconds (a negative integer) for a notification. Required only for historical representations.
Base Time	bt	No	The base current time which the Time values are relative to as a Time data type (See Appendix B)
Float Value	v	One value field is mandatory	Value as a JSON float if the Resource data type is integer or float.
Boolean Value	bv		Value as a JSON Boolean if the Resource data type is boolean.
String Value	sv		Value as a JSON string for all other Resource data types. If the Resource data type is opaque the string value holds the Base64 encoded representation of the Resource.
Table 17: JSON format and description

For example a request to Device Object of the LWM2M example client (Get /3/0) would return the following JSON payload. This example has a size of 397 bytes.

{“e”:[

{"n":"0","sv":"Open Mobile Alliance"},

{"n":"1","sv":"Lightweight M2M Client"},

{"n":"2","sv":"345000123"},

{"n":"3","sv":"1.0"},

{"n":"6/0","v":"1"},

{"n":"6/1","v":"5"},

{"n":"7/0","v":"3800"},

{"n":"7/1","v":"5000"},

{"n":"8/0","v":"125"},

{"n":"8/1","v":"900"},

{"n":"9","v":"100"},

{"n":"10","v":"15"},

{"n":"11/0","v":"0"},

{"n":"13","v":"1367491215"},

{"n":"14","sv":"+02:00"},

{"n":"15","sv":"U"}]

}

For example a notification about a Resource containing multiple historical representations of a Temperature Resource in the example could result in the following JSON payload:

{“e”:[

{"n":"1/2","v":"22.4","t":"-5"},

{"n":"1/2","v":"22.9","t":"-30"},

{"n":"1/2","v":"24.1","t":"-50"}],

"bt":"25462634"

}
