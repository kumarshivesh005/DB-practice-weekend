owners[icon:dollar-sign,color:blue]{
  owner_id SERIAL PK
  owner_name VARCHAR(50)
  wealth VARCHAR(50)
  about_owner TEXT
  created_at timestamp
  updated_at timestamp
}


teams[icon:teams,color:red]{
  team_id SERIAL PK
  owner_id INT FK
  team_name VARCHAR(50) 
  created_at timestamp
}


players[icon:play,color:green]{
  player_id SERIAL PK
  team_id INT FK
  player_name VARCHAR(50)
  role VARCHAR(50)
  bought_at timestamp
}


sponsors[icon:blockchain,color:green]{
  sponsor_id SERIAL PK
  team_id INT FK
  sponsor_name VARCHAR(20)
  price INT
  created_at timestamp

  
}


matches[icon:mastercard,color:green]{
  match_id SERIAL PK
  team1_id INT FK
  team2_id INT FK
  stadium_name VARCHAR(50)
  match_result VARCHAR(50)
  match_time timestamp
}
broadcasters[icon:aws-elemental-live,color: purple]{
  broadcaster_id SERIAL PK
  match_id INT FK
  broadcaster_name VARCHAR(50)
  created_at timestamp
}

// o-mt
owners.owner_id <teams.owner_id

// t-mp
 teams.team_id <players.team_id

// t-ms
teams.team_id <sponsors.team_id

teams.team_id <matches.team1_id
teams.team_id <matches.team2_id

// m-mb
matches.match_id <broadcasters.match_id


