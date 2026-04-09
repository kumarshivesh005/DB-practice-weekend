vehicles[icon:azure-connected-vehicle-platform,color:blue]{
  vehicle_id SERIAL PK
  vehicle_number VARCHAR(20)
  vehicle_owner_name VARCHAR(50)
  owner_email VARCHAR(322) unique not null
  owner_phone VARCHAR(12) unique
  vehiclecategorie_id INT FK
}


vehiclecategories[icon:car,color:blue]{
  vehiclecategorie_id SERIAL PK
  vehiclecategorie_name VARCHAR(50)
}


parkingzones[icon:parking]{
  parkingzone_id SERIAL PK
  vehiclecategorie_id INT FK
  parkingzone_name VARCHAR(50)
  parkingzone_level INT
  created_at timestamp
}


parkingspots[icon:parkingspot]{
  parkingspot_id SERIAL PK
  parkingzone_id INT FK
  parkingspotcategory_id INT FK
  is_vacent BOOLEAN
}


parkingspotcategories[icon:building]{
  parkingspotcategory_id SERIAL PK
  parkingspot_id INT FK
  parkingzone_id INT FK
  is_reserver BOOLEAN
  parkingspotcategory_name VARCHAR(20)
  parkingspotcategory_date timestamp
}


parkingtickets[icon:ticket]{
  parkingticket_id SERIAL PK
  vehicle_id INT FK
  parkingspot_id INT FK
  entered_at timestamp
  exited_at timestamp
}


parkingsessions[icon: timer]{
  parkingsession_id SERIAL PK
  vehicle_id INT FK
  parkingspot_id INT FK
  parkingticket_id INT FK
  entered_at timestamp
  exited_at timestamp
}


payments[icon:payment]{
  payment_id VARCHAR PK
  parkingsession_id INT FK
  payment_amount INT
  paymented_at timestamp
  payment_status BOOLEAN
  payment_method VARCHAR(20)

}
//1vc-mv
vehiclecategories.vehiclecategorie_id <vehicles.vehiclecategorie_id
//1vc-1pz
vehiclecategories.vehiclecategorie_id -parkingzones.vehiclecategorie_id
//1pz-1psc
parkingzones.parkingzone_id - parkingspotcategories.parkingzone_id
//1psc-mps
parkingspotcategories.parkingspotcategory_id < parkingspots.parkingspotcategory_id
//1pz-mps
parkingzones.parkingzone_id < parkingspots.parkingzone_id
//1ps-mpt
parkingspots.parkingspot_id < parkingtickets.parkingspot_id
//1ps-mps
parkingspots.parkingspot_id <parkingsessions.parkingspot_id

//1pt-mps
parkingtickets.parkingticket_id < parkingsessions.parkingticket_id

//1v-mps
vehicles.vehicle_id < parkingsessions.vehicle_id
//1ps-1pay
parkingsessions.parkingsession_id - payments.parkingsession_id
//1v-mpt
vehicles.vehicle_id < parkingtickets.vehicle_id
