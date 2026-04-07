// SQL DB code 

trainers[icon:user,color:blue]{
  trainer_id SERIAL PK
  name VARCHAR(50)
  email VARCHAR(322) unique not null
  phone VARCHAR(12)
  specification TEXT
}
clients[icon:user,color:yellow]{

  client_id SERIAL PK
  name VARCHAR(50)
  email VARCHAR(322) unique not null
  phone VARCHAR(12)
  createdAt timestamp

}


plans[icon:plant]{
  plan_id SERIAL PK
  name VARCHAR(50)
  trainer_id INT FK
  price INT 
  duration VARCHAR(20)
  description TEXT
  is_live enum
}

subscriptions[icon:azure-subscriptions]{
  subscription_id VARCHAR PK
  client_id INT FK
  plan_id INT FK
  started_date timestamp
  end_date timestamp

}

sessions[icon:timer,color:blue]{
  session_id SERIAL PK
  trainer_id INT FK
  started_at timestamp
  ened_at timestamp

}
clientsessions[icon:timer,color:yellow]{
  clientsession_id SERIAL PK
  session_id INT FK
  client_id INT FK
  subscription_id VARCHAR FK
  started_at timestamp
  ened_at timestamp
}

progresses[icon:arrow-up-down]{
  progresse_id SERIAL PK
  client_id INT FK
  clientsession_id INT FK
  isReport_submitted enum

}
payments[icon:money]{
  payment_id VARCHAR PK
  subscription_id VARCHAR FK
  client_id INT FK
  amount INT
  paid_at timestamp
  updatepayment_at timestamp
}
//mt-mc
clients.client_id <>trainers.trainer_id


//1t-mp
trainers.trainer_id < plans.trainer_id

//1t-msess
trainers.trainer_id <sessions.trainer_id




//1c-msub
clients.client_id <subscriptions.client_id

//1c-msessionclient bcz of multiple buy
clients.client_id <clientsessions.client_id
//1c-mprog
clients.client_id <progresses.client_id

//1p-1sub
plans.plan_id - subscriptions.plan_id



//msessclient-1session
sessions.session_id<clientsessions.session_id

//msessclient-1sub
subscriptions.subscription_id <clientsessions.subscription_id

//1sessclient-mprog
clientsessions.clientsession_id <progresses.clientsession_id



//1 payment-1 subs
payments.payment_id -subscriptions.payment_id



