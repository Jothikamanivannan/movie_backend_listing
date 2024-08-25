#app.js
require("dotenv").config();
const movieRoutes = require("./routes/movies/moviesRoutes");
const bookRoutes = require("./routes/movies/books");
const express = require("express");
const db = require("./db/index");
const app = express(); 
const port = process.env.PORT || 8080;
db()
app.use(express.json)

app.use("/movies", movieRoutes);
app.use("/book", bookRoutes);
db();
app.listen(port, () => {
    console.log(`Express app listening at http://localhost:${port}`);
});

#index.js
const mongoose = require("mongoose");
const connectDB = async () => {
    try {
        await mongoose.connect(process.env.MONGODB_URI);
        console.log(`MongoDB connected...`);
    }catch(err) {
        console.log(`MongoDB connection error:`,err);
        throw err;
    }
}

module.exports = connectDB;  

#.env
PORT=8080
MONGODB_URI = mongodb+srv://jothikamanivannan38:xkgJ4SM4UoUyk1sK@jothika.srsgm.mongodb.net/?retryWrites=true&w=majority&appName=Jothika

#package.json
{
  "name": "movie-listing-backend",
  "version": "1.0.0",
  "main": "index.js",
  "scripts": {
    "dev": "nodemon app.js"
  },
  "author": "Jothika",
  "license": "ISC",
  "description": "",
  "dependencies": {
    "dotenv": "^16.4.5",
    "express": "^4.19.2",
    "mongoose": "^8.5.4",
    "nodemon":"^3.1.4"
  }
}

#book.js
const express = require("express");
const router = express.Router();

router.post("/", (req, res) => {
  const { movieId, seatNumber } = req.body;
  res.json({ message: "Ticket booked successfully!", movieId, seatNumber });
});

module.exports = router;

#movieschema.js
const mongooese = require("mongoose");

const movieSchema = new mongooese.Schema({
  name: {
    type: String,
    required: true,
  },
  description: {
    type: String,
    required: true,
  },
  releaseDate: {
    type: Date,
    required: true,
  },
  genre: {
    type: String,
    required: false,
  },
  duration: {
    type: Number,
    required: true,
  },
  rating: {
    type: Number,
    required: true,
  },
});

const Movie = mongooese.model("Movie", movieSchema);

module.exports = Movie;

#lauch.json
//use intellisence to learn about possible attributes,
    //hover to view descriptions of existing attributes,
    //for more information,visit://https://go.microsoft.com/fwlink/?linkid=830387
    "version":"0.2.0",
    "configurations": [
        {
            "type":"chrome",
            "request":"launch",
            "name":"launch chrome again location",
            "url":"https://localhost:8080",
            "webRoot":"${workspaceFolder}"
          }
    ]
}
