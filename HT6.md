# HT 6

### Airlines
#### 1
###### Query:
```javascript
db.airlines.aggregate([
    {
        $group: {
            _id: {
                class: "$class"
            },
            total: { $sum: 1}
        }
    },
    {
        $project : {
            _id : 0,
            class: "$_id.class",
            total : "$total"
        }
    }
])
```
###### Result:
```javascript
{ "class" : "F", "total" : 140343 }
{ "class" : "L", "total" : 23123 }
{ "class" : "P", "total" : 5683 }
{ "class" : "G", "total" : 17499 }
```
---

#### 2
###### Query:
```javascript
db.airlines.aggregate([
    {
        $match: {
            destCountry: { $not: {$eq: "United States"} }
        }
    },
    {
        $group: {
            _id: {
                destCity: "$destCity"
            },
            avgPassengers: { $avg: "$passengers"}
        }
    },
    {
        $project: {
            _id: 0,
            avgPassengers: "$avgPassengers",
            city: "$_id.destCity"
        }
    },
    {
        $sort: {
            avgPassengers: -1
        }
    },
    {
        $limit: 3
    }
])
```
###### Result:
```javascript
{ "avgPassengers" : 8052.380952380952, "city" : "Abu Dhabi, United Arab Emirates" }
{ "avgPassengers" : 7176.596638655462, "city" : "Dubai, United Arab Emirates" }
{ "avgPassengers" : 7103.333333333333, "city" : "Guangzhou, China" }
```
---