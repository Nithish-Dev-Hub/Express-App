const express = require("express"); 

//Express app mounting
const app = express();

app.use(express.json());

let finalArr = [
    {
        from: "vendor 1",
        location: "Chennai",
        product: "watch-1",
        price: 149
    },
    {
        from: "vendor 2",
        location: "Hyderabad",
        product: "watch-2",
        price: 1499
    },
    {
        from: "vendor 3",
        location: "Hyderabad",
        product: "watch-3",
        price: 249
    },
    {
        from: "vendor 4",
        location: "Bangalore",
        product: "watch-4",
        price: 14999
    },
    {
        from: "vendor 5",
        location: "Bangalore",
        product: "watch-5",
        price: 3449
    },
  
];
let finalVal = {
    from: "",
    location: "",
    product: "",
    description: "",
    price: 0
};

app.get("/getdata", (req, res)=> {
    res.send(finalArr);
});

app.post("/setdata", (req, res)=> {
    finalVal = req.body;
    finalArr.push(finalVal);
    res.send(req.body);
});

app.delete("/deletedata/:tag", (req, res)=> {
    console.log(req.url, req.params, req.query);
    let id = req.query.id;
    let tag = req.params.tag;
    let targetVAlue = finalArr.findIndex(item => item[tag] === id);
    let tempVal = finalArr.splice(targetVAlue,1);

    console.log(targetVAlue, tempVal);
    res.send(finalArr);
});

let PORT = 8080;

app.listen(PORT, () =>{
    console.log(`Express Server Ready at http://localhost:${PORT}`);
});