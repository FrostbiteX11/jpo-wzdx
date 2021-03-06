# lanes
**Optional**

This table identifies and describes individual lanes within a road event. Each entry in this table represents a single lane.

This table is related to the [road_events](/spec-content/data-tables/road_events.md) table by the foreign key `road_event_id`.  For every record in the `road_event` table there may exist zero or more related record(s) in the `lanes` table. In the GeoJSON feed output, each lane record will map to one lane object on the `lanes` array in the road event properties.

This table is related to the [lane_restrictions](/spec-content/data-tables/lane_restrictions.md) table. For each record in the `lanes` table there may exist one or more records in the `lane_restrictions` table.  The `lane_id` field acts as the foreign key in the `lanes` table.

## Lanes Table Structure
Field Name | Data Type | Description | Conformance | Notes
--- | --- | --- | --- | ---
lane_id | ID | Identifies the lane record. | Required | Primary key
[road_event_id](/spec-content/data-tables/road_events.md) | ID | Identifies the road event to which a lane information is related. | Required | Foreign key
order | Positive Integer | The position of a lane in sequence on the roadway. This value is used as an index to indicate the order of all WZDx lanes provided for a road event. | Required | A value of `1` must represent the **left-most** lane and an increase in 1 must represent moving a single lane over from the **left**.
type | Enumeration; Text | An indication of the type of lane or shoulder. | Required | See [Lane Type Enumerated Type](/spec-content/enumerated-types/derived-from-its-standards/lane_type.md)
status | Enumeration; Text | Status of the lane for the traveling public. | Required | See [Lane Status Enumerated Type](/spec-content/enumerated-types/lane_status.md)
lane_number | Positive Integer | The number assigned to the lane to help identify its position. Flexible, but usually used for regular, driveable lanes. | Optional | Assigned by counting from the **left** edge of the improved surface. Useful for text to voice translation.
