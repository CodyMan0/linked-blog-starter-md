
```
const movieAPI = "https://movieapi.com/data";

const tvAPI = "https://tvapi.com/data";

​

const getData = () => {

return Promise.all([

fetch(movieAPI),

fetch(tvAPI)

])

.then(([movieRes, tvRes]) => {

return Promise.all([movieRes.json(), tvRes.json()])

})

.then(([movieJson, tvJson]) => {

return {

movies: movieJson,

tvs: tvJson

}

})

}
```