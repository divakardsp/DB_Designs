# 🏋️ Fitness Influencer Coaching Platform

## 📌 Overview

This project focuses on designing a database schema for an **online fitness coaching platform** where trainers (fitness influencers) manage clients digitally.

The platform supports:

* Client onboarding
* Coaching plan management
* Subscriptions and payments
* Consultations (video sessions)
* Daily check-ins and progress tracking


## 🧾 ER Diagram Code

> ⚠️ Note: The ER diagram becomes visually cluttered due to multiple relationships.
> For clarity and reproducibility, the code representation is shared below.

```
// =====================
// TRAINERS
// =====================
trainers{
  trainer_id string pk
  name string not_null
  age number not_null
  gender enum( Male Female Others) not_null 
  phone_number string not_null
  email string not_null
  password string not_null
  rating number 
  createdAt timestamp
  updatedAt timestamp
}

// =====================
// CLIENTS
// =====================
clients{
  client_id string pk
  name string not_null
  age number not_null
  gender enum( Male Female Others) not_null 
  phone_number string not_null
  email string not_null
  password string not_null
  progress_id string fk
  trainer string fk 
  subscriptions string[] fk
  consultations string[] fk
  workout_plan string fk
  diet_plan string fk
  createdAt timestamp
  updatedAt timestamp
}

// =====================
// WORKOUT PLANS
// =====================
workout_plans{
  workout_plan_id string pk
  goal enum( FatLoss Strength GeneralFitness WeightGain) not_null
  CardioDays string[]
  StrengthTrainingDays string[]
  Exercises object
  DesignedBy string fk
  createdAt timestamp
  updatedAt timestamp
}

// =====================
// DIET PLANS
// =====================
diet_plans{
  diet_plan_id string pk
  goal enum( FatLoss MuscleGain Strength GeneralFitness) not_null
  maintenance_cal number not_null
  calorie_intake number not_null
  protein string not_null
  carbs string not_null
  createdAt timestamp
  updateAt timestamp
}

// =====================
// PROGRESS
// =====================
progresses{
  progress_id string pk
  inital_weight number not_null
  current_weight number
  initial_body_fat_percentage number
  current_body_fat_percentage number
  category enum (UnderWeight NormalWeight OverWeight Obesity)
  daily_check_ins string[] fk
  createdAt timestamp
  updatedAt timestamp
}

// =====================
// DAILY CHECK-INS
// =====================
daily_check_ins{
  check_in_id string pk
  client_id string fk
  date Date not_null
  weight number 
  calorie_intake object (breakfast,lunch, dinner)
  steps number
  calorie_burnt number
  createdAt timestamp
  updatedAt timestamp
}

// =====================
// SUBSCRIPTIONS
// =====================
subscriptions{
  subscription_id string pk
  name string not_null
  description text not_null
  amount number not_null
  starting_date Date not_null
  end_date Date not_null
  trainers string[] fk
  category enum(FatLoss Strength GeneralFitness WeightGain)
  isOnline boolean
  createdAt timestamp
  updatedAt timestamp
}

// =====================
// CONSULTATIONS
// =====================
consultations{
  consultation_id string pk
  consultee string fk not_null
  consultingTo string fk not_null
  amount number not_null
  date DateTime not_null
  createdAt timestamp
  updatedAt timestamp
}

// =====================
// PAYMENTS
// =====================
payments{
  payment_id string pk
  isSubscription boolean not_null
  subscription_id string fk
  consultation_id string fk
  amount number 
  transaction_id string 
  status enum(Pending Success Failed)
  mode enum(UPI COD Card)
  createdAt timestamp
  updatedAt timestamp
}

// =====================
// RELATIONSHIPS
// =====================
clients.progress_id - progresses.progress_id
clients.trainer > trainers.trainer_id
clients.workout_plan - workout_plans.workout_plan_id
clients.diet_plan - diet_plans.diet_plan_id
clients.consultations > consultations.consultation_id
clients.subscriptions > subscriptions.subscription_id

workout_plans.DesignedBy  - trainers.trainer_id

daily_check_ins.client_id > clients.client_id

progresses.daily_check_ins < daily_check_ins.check_in_id

subscriptions.trainers < trainers.trainer_id

consultations.consultee - clients.client_id
consultations.consultingTo - trainers.trainer_id

payments.subscription_id - subscriptions.subscription_id
payments.consultation_id - consultations.consultation_id
```

---


## 🚀 Submission Details

This repository contains:

* ER diagram (code format)
* Complete schema design
* Explanation of entities and relationships

---
