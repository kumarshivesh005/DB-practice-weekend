doctors[icon:doctor,color:blue]{
  doctor_id SERIAL PK
  doctor_name VARCHAR(50)
  email VARCHAR(322) unique not null
  phone VARCHAR(12) unique
  specialities TEXT
  created_at timestamp
}

patients[icon:user]{
  patient_id SERIAL PK
  patient_name VARCHAR(50)
  email VARCHAR(322) unique not null
  phone VARCHAR(12) unique
  address TEXT
  age INT
  weight INT
  symyom TEXT
  appointment_status enum
  created_at timestamp
}

appointments[icon:aws-connect]{
  appointment_id SERIAL PK
  patient_id INT FK
  doctor_id INT FK
  price INT
  appointment_date timestamp
}
consultations[icon:consul]{
  consultation_id SERIAL PK
  appointment_id INT FK
  doctor_id INT FK
  consultation_note TEXT
  consultation_date timestamp
}

diagnostictests[icon:test-tube]{
  diagnostictest_id SERIAL PK
  consultation_id INT FK
  name VARCHAR(20)
  price INT
  diagnostictest_date timestamp
}

reports[icon: report]{
  report_id SERIAL PK
  diagnostictest_id INT FK
  doctor_id INT FK
  report_result TEXT
  report_date timestamp
}

payments[icon:payment]{
  payment_id VARCHAR PK
  appointment_id INT FK
  diagnostictest_id INT FK
  payment_amount INT
  paymented_at timestamp
  payment_status BOOLEAN
  payment_method VARCHAR(20)

}

//1p-Ma
patients.patient_id < appointments.patient_id


//1d0c-ma
doctors.doctor_id < appointments.doctor_id


//1a-0/1c
appointments.appointment_id - consultations.appointment_id


//1doc-mc
doctors.doctor_id < consultations.doctor_id


//1doc-mr
doctors.doctor_id <reports.doctor_id


//1c-mt
consultations.consultation_id < diagnostictests.consultation_id


//1t-Mr
diagnostictests.diagnostictest_id  < reports.diagnostictest_id





//1a-1pay
appointments.appointment_id - payments.appointment_id


//1t-1pay
diagnostictests.diagnostictest_id - payments.diagnostictest_id



