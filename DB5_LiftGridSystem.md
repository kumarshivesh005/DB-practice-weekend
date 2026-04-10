buildings[icon:building,color:blue]{
  building_id SERIAL PK
  building_name VARCHAR(50)
  building_address VARCHAR(50)
  about_building TEXT
}


floors[icon:flowchart,color:blue]{
  floor_id SERIAL PK
  numberof_floor INT
  building_id INT FK
}


elevators[icon:elevenlabs]{
  elevator_id SERIAL PK
  building_id INT FK
  floor_id INT FK
  elevatorshaft_id INT FK
  numberof_elevator INT
}


elevatorshafts[icon:bolt]{
  elevatorshaft_id SERIAL PK
  building_id INT FK
  numberof_elevatorshaft INT
}


floorrequests[icon:folder]{
  floorrequest_id SERIAL PK
  floor_id INT FK
  elevator_id INT FK
  rideassignment_id INT FK
}
rideassignments[icon:assignment]{
  rideassignment_id SERIAL PK
  floorrequest_id INT FK
  elevator_id INT FK
  trip_id INT FK
  assigned_at timestamp
}


trips[icon:train]{
  trip_id SERIAL PK
  elevator_id INT FK
  floorrequest_id INT FK
  elevatorstatus_id INT FK
  numberof_trip INT
  started_at timestamp
  ended_at timestamp
}


elevatorstatuses[icon: stream]{
  elevatorstatus_id SERIAL PK
  maintaince_id INT FK
  is_working BOOLEAN
}


maintainces[icon:timer]{
  maintaince_id SERIAL PK
  elevator_id INT FK
  
  maintainced_at timestamp
}
// b-me
buildings.building_id <elevators.building_id

// b-mf
buildings.building_id <floors.building_id

// b-mes
buildings.building_id <elevatorshafts.building_id

// f-me
floors.floor_id <elevators.floor_id
// f-mfr
floors.floor_id <floorrequests.floor_id

// 1es-1e
elevatorshafts.elevatorshaft_id - elevators.elevatorshaft_id

// es-1main
elevatorshafts.elevatorshaft_id -maintainces.elevatorshaft_id


// e-mfr
elevators.elevator_id <floorrequests.elevator_id

// fr-mt
floorrequests.floorrequest_id <trips.floorrequest_id
// e-mt
elevators.elevator_id <trips.elevator_id

// est-mt
elevatorstatuses.elevatorstatus_id < trips.elevatorstatus_id

// m-1e
elevators.elevator_id - maintainces.elevator_id

//1e-1rideassi
elevators.elevator_id - rideassignments.elevator_id
//1t-mrassi
trips.trip_id <rideassignments.trip_id

// 1rassi-mfr
rideassignments.rideassignment_id <floorrequests.rideassignment_id


