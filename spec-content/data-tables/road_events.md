# road_events
**Required**

This table  contains information about work zone events.  The information describes where, when, and what activity is taking place along a road segment. This specification currently accommodates work zones; This design accommodates multiple road event types.

This table is related to the [road_event_data_sources](/spec-content/data-tables/road_event_data_sources.md) table by the foreign key `data_source_id`. For every record in the `road_event_data_sources` table there must exist one or more `road_event` records.

This table is related to the [types_of_work](/spec-content/data-tables/types_of_work.md) table. For each record in the `road_events` table there may exist zero or more records in the `types_of_work` table. The `road_event_id` field acts as the foreign key in the `types_of_work` table.

This table is related to the [lanes](/spec-content/data-tables/lanes.md) table. For each record in the `road_events` table there may exist zero or more related record(s) in the `lanes` table. The `road_event_id` field acts as the foreign key in the `lanes` table. In the GeoJSON feed output, each lane record will map to one lane object on the `lanes` array in the road event properties.

This table is related to the [relationships](/spec-content/data-tables/relationships.md) table. For each record in the `road_events` table there may exist one record in the `relationships` table. The `road_event_id` field acts as the foreign key in the `relationships` table.

## Road Events Table Structure
Field Name | Data Type | Description | Conformance | Notes
--- | --- | --- | --- | ---
**road_event_id** | ID | An unique identifier issued by the data feed provider to identify the work zone project or activity. | Required | Primary Key
**event_type** | Enumeration; Text | The type/classification of road event. | Required | See [Event Type Enumerated Type](/spec-content/enumerated-types/event_type.md)
**data_source_id** | ID | Identifies the data source from which the road event originates. | Required | Foreign Key to [road_event_data_sources](/spec-content/data-tables/road_event_data_sources.md) `data_source_id`
**geometry_type** | Enumeration: Multipoint or LineString | May be represented as a linestring or a multipoint as defined in the GeoJSON specification. | Required |
**geometry**|Coordinate(s); Float | A coordinate pair or an array of coordinates. In either case, the first coordinate is the beginning point and the last coordinate is the ending point of the road event. | Required | Coordinate pairs and coordinate arrays are formatted according to the GeoJSON spec
**road_name** | Text | Publicly known name of the road on which the event occurs. | Required |
**road_number** | Text | The road number designated by a jurisdiction such as a county, state, or interstate. | Optional | Examples I-5, VT 133
**direction** | Enumeration; Text | The digitization direction of the road that is impacted by the event. This value is based on the standard naming for US roadways and indicates the direction of the traffic flow regardless of the real heading angle.  | Required | Example `northbound` (for I-5 North); See [Direction Enumerated Type](/spec-content/enumerated-types/derived-from-its-standards/direction.md)
**beginning_cross_street** | Text | Name or number of the nearest cross street along the roadway where the event begins. | Optional |
**ending_cross_street** | Text | Name or number of the nearest cross street along the roadway where the event ends. | Optional |
**beginning_milepost** | Float | The linear distance measured against a milepost marker along a roadway where the event begins. | Optional | 	A milepost or mile marker is a surveyed distance posted along a roadway measuring the length (in miles or tenth of a mile) from the south west to the north east. These markers are typically notated on State and local government digital road networks. Provide link to description of milepost method in metadata file.
**ending_milepost** | Float | The linear distance measured against a milepost marker along a roadway where the event ends. | Optional | A milepost or mile marker is a surveyed distance posted along a roadway measuring the length (in miles or tenth of a mile) from the south west to the north east. These markers are typically notated on State and local government digital road networks. Provide link to description of milepost method in metadata file.
**beginning_accuracy** | Enumeration; Text | Indicates how the beginning coordinate was defined. | Required | See [Spatial Verification Enumerated Type](/spec-content/enumerated-types/spatial_verification.md)
**ending_accuracy** | Enumeration; Text | Indicates how the ending coordinate was defined. | Required | See [Spatial Verification Enumerated Type](/spec-content/enumerated-types/spatial_verification.md)
**start_date** | DateTime | The UTC time and date when the event begins. | Required | All datetime formats shall follow [RFC 3339 Section 5.6](https://tools.ietf.org/html/rfc3339#section-5.6). Example: `2016-11-03T19:37:00Z`
**end_date** | DateTime | The UTC time and date when the event ends. | Required | All datetime formats shall follow [RFC 3339 Section 5.6](https://tools.ietf.org/html/rfc3339#section-5.6). Example: `2016-11-03T19:37:00Z`
**start_date_accuracy** | Enumeration; Text | A measure of how accurate the start Date Time is. | Required | See [Time Verification Enumerated Type](/spec-content/enumerated-types/time_verification.md)
**end_date_accuracy** | Enumeration; Text | A measure of how accurate the end Date Time is. | Required | See [Time Verification Enumerated Type](/spec-content/enumerated-types/time_verification.md)
**event_status**  | Enumeration; Text | The status of the event. | Optional | See [Event Status Enumerated Type](/spec-content/enumerated-types/event_status.md)
**total_num_lanes**  | Integer | The total number of lanes associated with the road segment designated by the event geometry. | Optional | A segment is a part of a roadway in a single direction designated the event geometry
**vehicle_impact** | Enumeration; Text | The impact to vehicular lanes along a single road in a single direction. | Required | See [Vehicle Impact Enumerated Type](/spec-content/enumerated-types/vehicle_impact.md)
**workers_present** | Boolean | A flag indicating that there are workers present in the event space. | Optional
**reduced_speed_limit** | Integer | The reduced speed limit posted within the event space. | Optional |
**restrictions** | Enumumeration; Text | Zero or more road restrictions applying to the work zone road segment associated with the work zone delimited by semicolons. | Optional | These are included as flags rather than detailed restrictions. Detailed restrictions are coded to specific lanes in the lane_restrictions table. See [Road Restriction Enumerated Type](/spec-content/enumerated-types/road_restriction.md)
**description** | Text | Short free text description of work zone. | Optional | This will be populated with formal phrases in a later WZDx version
**creation_date** | DateTime | The UTC time and date when the activity or event was created. | Optional | All datetime formats shall follow [RFC 3339 Section 5.6](https://tools.ietf.org/html/rfc3339#section-5.6). Example: `2016-11-03T19:37:00Z`
**update_date** | DateTime | The UTC time and date when the activity or event was updated. | Optional | All datetime formats shall follow [RFC 3339 Section 5.6](https://tools.ietf.org/html/rfc3339#section-5.6). Example: `2016-11-03T19:37:00Z`
