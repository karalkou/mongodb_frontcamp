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