# hackathon
Topic ID - CBP33
Title - Student Innovation
Category - Travel and Tourism

HTML - section 
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Yatra Saathi</title>
    <link rel="stylesheet" href="Hackathon CSS.css">
</head>
<body>
    <div class="container">
        <form action="https://www.google.com/search" target="_blank" method="get" class="search-bar">
            <input type="text" placeholder="Search" name="q">
            <button type="submit"><img src="search.png"></button>
        </form>
    </div>
</body>
</html>


This is an HTML document for a tourism website. It includes a form where users can input a destination name to get details about that destination. Upon submitting the form, it fetches data from the server using JavaScript's Fetch API, then displays the destination details dynamically on the page without refreshing. The details include the destination's name, description, location, attractions, photo, nearest train station, and nearest bus station, all hotels and its prices. The styling is done using CSS to create a visually appealing layout with a container, form, and various elements formatted for better user experience.


 css - section

 {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
    font-family: 'sans-serif';
}

.container{
    width: 100%;
    min-height: 100vh;
    padding: 2%;
    background-image: linear-gradient(rgba(10, 0, 0, 0.9),rgba(0,8,51,0.9)), url("background.jpg");
    background-position: center;
    background-size: cover;
    display: flex;
    align-items: flex-start;
    justify-content: center;
}
.search-bar{
    width: 100%;
    max-width: 700px;
    background: rgba(255, 255, 255, 0.2);
    display: flex;
    align-items: center;
    border-radius: 60px;
    padding: 10px 20px;
    backdrop-filter: blur(4px) saturate(180%);
}

.search-bar input{
    background: transparent;
    flex: 1;
    border: 0;
    outline: none;
    padding: 24px 20px;
    font-size: 20px;
    color: #cac7ff;
}
::placeholder{
    color: #cac7ff;
}

.search-bar button img{
    width: 35px
}

.search-bar button{
    border: 0;
    border-radius: 50%;
    width: 60px;
    height: 60px;
    background: #58629b;
    cursor: pointer;
}

This is a CSS stylesheet defining styles for a search bar within a container. The container occupies the full width and minimum height of the viewport, with a background gradient and image. The search bar itself is a flex container with a maximum width of 700px, positioned in the center of the container. It features a translucent background, rounded corners, and a blur effect. The input field occupies most of the width, with placeholder text and a font size of 20px. The search button has a circular shape, background color, and an image for visual indication. Overall, the design aims for a modern and visually appealing search interface. This website make very easy for every user to plan a vacation in that city to boost travel and tourism industry.


AFTER THIS

we have to import required modules for backend;
which are express,mangoose. 
After that ;
// Import required modules
const express = require('express');
const mongoose = require('mongoose');

// Create an Express application
const app = express(); 

connect to database to save data

// Connect to MongoDB database
mongoose.connect('mongodb://localhost:27017/tourismDB', { useNewUrlParser: true, useUnifiedTopology: true });
const db = mongoose.connection;

// Define schemas for tourism destinations and train/bus stations
AND add more details and connect further

![79](https://github.com/Dn670/hackathon/assets/151924437/807b4df1-4337-4df2-85f0-e2627c308bda)

here we are adding our basic code of backend which would further add more features

const express = require('express');
const mongoose = require('mongoose');


const app = express();


mongoose.connect('mongodb://localhost:27017/tourismDB', { useNewUrlParser: true, useUnifiedTopology: true });
const db = mongoose.connection;

const destinationSchema = new mongoose.Schema({
    name: String,
    description: String,
    location: String,
    attractions: [String],
    photoUrl: String,
    nearestTrainStation: String,
    nearestBusStation: String
});

const trainStationSchema = new mongoose.Schema({
    name: String,
    location: String,
    timings: [String],
    tickets: String
});

const busStationSchema = new mongoose.Schema({
    name: String,
    location: String,
    timings: [String]
});


const Destination = mongoose.model('Destination', destinationSchema);
const TrainStation = mongoose.model('TrainStation', trainStationSchema);
const BusStation = mongoose.model('BusStation', busStationSchema);

app.use(express.json());

app.get('/destination/:name', async (req, res) => {
    try {
        const destination = await Destination.findOne({ name: req.params.name });
        if (!destination) {
            return res.status(404).json({ message: 'Destination not found' });
        }
        res.json(destination);
    } catch (err) {
        res.status(500).json({ message: err.message });
    }
});


app.get('/train-station/:name', async (req, res) => {
    try {
        const trainStation = await TrainStation.findOne({ name: req.params.name });
        if (!trainStation) {
            return res.status(404).json({ message: 'Train station not found' });
        }
        res.json(trainStation);
    } catch (err) {
        res.status(500).json({ message: err.message });
    }
});


app.get('/bus-station/:name', async (req, res) => {
    try {
        const busStation = await BusStation.findOne({ name: req.params.name });
        if (!busStation) {
            return res.status(404).json({ message: 'Bus station not found' });
        }
        res.json(busStation);
    } catch (err) {
        res.status(500).json({ message: err.message });
    }
});


const PORT = process.env.PORT || 3000;
app.listen(PORT, () => {
    console.log(`Server is listening on port ${PORT}`);
});
