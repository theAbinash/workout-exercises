# Workout Exercises

A structured and reusable exercise dataset containing exercise information, descriptions, body parts, equipment, exercise categories, tracking types, and keywords.

This repository is designed to provide a centralized exercise data source that can be consumed by fitness, workout-tracking, health, and training applications.

## Overview

The dataset is primarily maintained in `exercises.json`.

Each exercise contains information that can be used for:

* Exercise selection
* Workout planning
* Exercise search
* Muscle/body-part filtering
* Equipment-based filtering
* Exercise categorization
* Workout tracking
* Repetition, weight, duration, and distance tracking
* Exercise recommendations
* Fitness application development

## Repository Structure

```text
workout-exercises/
│
├── exercises.json
├── images/
├── videos/
└── README.md
```

### `exercises.json`

The main exercise dataset containing structured information for each exercise.

### `images/`

Contains exercise-related image assets where available.

### `videos/`

Contains exercise-related video assets where available.

## Dataset Structure

The JSON file contains a `data` array, with each object representing an exercise.

Example:

```json
{
  "exercise_id": 1,
  "exercise_name": "Cable Single Arm Hammer Curl",
  "exercise_description": "A bicep isolation movement performed using a cable machine with a rope attachment or the cable end.",
  "exercise_image_url": "",
  "exercise_body_parts": [
    "BICEPS",
    "FOREARMS"
  ],
  "exercise_equipments": [
    "CABLE MACHINE"
  ],
  "exercise_type_id": 2,
  "exerciseType": "STRENGTH",
  "keywords": []
}
```

## Exercise Fields

| Field                  | Type    | Description                                          |
| ---------------------- | ------- | ---------------------------------------------------- |
| `exercise_id`          | Integer | Unique identifier for the exercise                   |
| `exercise_name`        | String  | Name of the exercise                                 |
| `exercise_description` | String  | Detailed description of the exercise                 |
| `exercise_image_url`   | String  | URL or reference for the exercise image              |
| `exercise_body_parts`  | Array   | Body parts or muscle groups targeted by the exercise |
| `exercise_equipments`  | Array   | Equipment required for the exercise                  |
| `exercise_type_id`     | Integer | Defines how the exercise should be tracked           |
| `exerciseType`         | String  | Exercise category/type such as `STRENGTH`            |
| `keywords`             | Array   | Search and filtering keywords                        |

## Exercise Categories

The `exerciseType` field represents the **general category of the exercise**.

For example:

```text
STRENGTH
```

This field should not be confused with `exercise_type_id`.

`exercise_type_id` defines the metrics that should be recorded while performing the exercise.

## Exercise Tracking Types

The `exercise_type_id` field determines what information should be collected when a user performs an exercise.

The supported tracking types are:

|  ID | Tracking Type     | Metrics                |
| --: | ----------------- | ---------------------- |
| `1` | Reps Only         | Repetitions            |
| `2` | Weight + Reps     | Weight and repetitions |
| `3` | Weight + Duration | Weight and duration    |
| `4` | Duration Only     | Duration               |
| `5` | Distance Only     | Distance               |
| `6` | Distance + Weight | Distance and weight    |

### 1. Reps Only

```text
exerciseTypeWithReps = 1
```

Used when the exercise is primarily tracked by the number of repetitions.

Example:

```text
Push Ups
Squats
Bodyweight Lunges
```

Tracked data:

```text
Reps: 15
```

### 2. Weight + Reps

```text
exerciseTypeWithWeightAndReps = 2
```

Used when both the weight and number of repetitions need to be recorded.

Example:

```text
Bench Press
Bicep Curl
Cable Single Arm Hammer Curl
```

Tracked data:

```text
Weight: 20 kg
Reps: 12
```

### 3. Weight + Duration

```text
exerciseTypeWithWeightAndDuration = 3
```

Used when an exercise requires both a weight/load and a duration.

Tracked data:

```text
Weight: 10 kg
Duration: 60 seconds
```

### 4. Duration Only

```text
exerciseTypeWithDurationOnly = 4
```

Used when the primary measurement is time.

Example:

```text
Plank
Wall Sit
Static Hold
```

Tracked data:

```text
Duration: 45 seconds
```

### 5. Distance Only

```text
exerciseTypeWithDistanceOnly = 5
```

Used when the exercise is primarily measured by distance.

Example:

```text
Running
Walking
Cycling
```

Tracked data:

```text
Distance: 5 km
```

### 6. Distance + Weight

```text
exerciseTypeWithDistanceAndWeight = 6
```

Used when both distance and weight need to be recorded.

Tracked data:

```text
Distance: 100 m
Weight: 20 kg
```

## Body Parts

The `exercise_body_parts` field contains the body parts or muscle groups targeted by an exercise.

Example:

```json
"exercise_body_parts": [
  "BICEPS",
  "FOREARMS"
]
```

This makes it possible to filter exercises based on the target muscle group.

Example use cases:

```text
Find all BICEPS exercises
Find all CHEST exercises
Find all BACK exercises
Find all LEG exercises
```

## Equipment

The `exercise_equipments` field contains the equipment required to perform an exercise.

Example:

```json
"exercise_equipments": [
  "CABLE MACHINE"
]
```

This can be used to build equipment-based exercise filters.

For example:

```text
Exercises using:
- Barbell
- Dumbbell
- Cable Machine
- Machine
- Kettlebell
- Bodyweight
```

## Keywords

The `keywords` field contains searchable terms associated with an exercise.

Example:

```json
"keywords": [
  "bicep",
  "curl",
  "hammer curl",
  "cable"
]
```

Keywords can be used to implement:

* Exercise search
* Autocomplete
* Related exercise suggestions
* Search filtering
* Exercise discovery

## Media

Exercise media can be associated with the dataset through the available image and video resources.

The dataset also contains the `exercise_image_url` field:

```json
"exercise_image_url": ""
```

Applications can use this field to resolve the appropriate image resource for an exercise.

The repository also provides dedicated directories for media:

```text
images/
videos/
```

## Using the Dataset

The dataset can be consumed by applications written in different technologies.

### JavaScript

```javascript
const exercises = require("./exercises.json");

const data = exercises.data;

console.log(data);
```

### Python

```python
import json

with open("exercises.json", "r", encoding="utf-8") as file:
    exercises = json.load(file)

data = exercises["data"]

for exercise in data:
    print(exercise["exercise_name"])
```

### Dart / Flutter

```dart
import 'dart:convert';
import 'dart:io';

final file = File('exercises.json');
final content = await file.readAsString();

final jsonData = jsonDecode(content);
final exercises = jsonData['data'];

for (final exercise in exercises) {
  print(exercise['exercise_name']);
}
```

## Filtering Examples

### Filter by Body Part

```dart
final bicepsExercises = exercises.where(
  (exercise) =>
      exercise.exerciseBodyParts.contains('BICEPS'),
);
```

### Filter by Equipment

```dart
final cableExercises = exercises.where(
  (exercise) =>
      exercise.exerciseEquipments.contains('CABLE MACHINE'),
);
```

### Filter by Tracking Type

```dart
final weightAndRepExercises = exercises.where(
  (exercise) =>
      exercise.exerciseTypeId == 2,
);
```

## Recommended Application Model

When integrating this dataset into a workout application, the exercise category and tracking type should be treated as two separate concepts.

```text
Exercise
│
├── Basic Information
│   ├── ID
│   ├── Name
│   └── Description
│
├── Target Information
│   ├── Body Parts
│   └── Equipment
│
├── Classification
│   └── Exercise Type
│
├── Tracking Configuration
│   └── Exercise Type ID
│
└── Search
    └── Keywords
```

For example:

```text
Exercise:
Cable Single Arm Hammer Curl

Category:
STRENGTH

Body Parts:
BICEPS
FOREARMS

Equipment:
CABLE MACHINE

Tracking Type:
WEIGHT + REPS

Tracking ID:
2
```

This separation allows the same exercise category to contain exercises with different tracking requirements.

## Data Validation

Before consuming the dataset, applications should validate:

* `exercise_id` is unique
* `exercise_name` is present
* `exercise_description` is valid
* `exercise_body_parts` is an array
* `exercise_equipments` is an array
* `exercise_type_id` contains a supported tracking type
* `exerciseType` contains a valid exercise category
* `keywords` is an array
* Media references resolve correctly where provided

## Integration Considerations

When using this dataset in a production application:

1. Treat `exercise_id` as the stable exercise identifier.
2. Use `exercise_type_id` to determine the workout tracking UI.
3. Use `exerciseType` for exercise categorization.
4. Use `exercise_body_parts` for muscle/body-part filtering.
5. Use `exercise_equipments` for equipment filtering.
6. Use `keywords` for search functionality.
7. Keep media resources synchronized with the exercise records.
8. Validate the JSON before importing or publishing new data.

## Example Workout Tracking Flow

A consuming application can use the dataset to dynamically determine the workout UI.

```text
Select Exercise
       │
       ▼
Read exercise_type_id
       │
       ├── 1 → Reps
       │
       ├── 2 → Weight + Reps
       │
       ├── 3 → Weight + Duration
       │
       ├── 4 → Duration
       │
       ├── 5 → Distance
       │
       └── 6 → Distance + Weight
```

This approach avoids hardcoding tracking fields for individual exercises.

## Contributing

Contributions are welcome.

When adding or modifying exercises:

1. Keep the JSON structure consistent.
2. Use a unique `exercise_id`.
3. Provide a clear exercise name.
4. Add a meaningful description.
5. Assign the appropriate body parts.
6. Assign the required equipment.
7. Select the correct `exercise_type_id`.
8. Assign the appropriate `exerciseType` category.
9. Add relevant keywords.
10. Add or update media resources where applicable.
11. Validate the JSON before committing changes.

## Data Design Principles

The dataset is designed around a simple principle:

> **Exercise information describes the movement; tracking information describes how the movement is measured.**

For example:

```text
Exercise Category
        │
        ▼
     STRENGTH
        │
        ▼
Tracking Type
        │
        ▼
   WEIGHT + REPS
        │
        ▼
Application Input
        │
        ├── Weight
        └── Repetitions
```

This separation makes the dataset flexible enough to support different workout-tracking experiences.

## License

Refer to the repository's license information before using the dataset in commercial or public applications.

## Maintainer

Maintained by `theAbinash`.

---

**Workout Exercises** — A structured exercise dataset for building workout, fitness, and exercise-tracking applications.
