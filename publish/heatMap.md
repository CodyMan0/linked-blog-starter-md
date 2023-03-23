
# 기상, 취침 Tracker

```dataviewjs
dv.span("** wakeUp traker**") 
const calendarData = {
    year: 2022, 
    colors: {  
	    blue:["#8cb9ff", "#69a3ff","#428bff", "#1872ff", "#0058e2"]
    },
    showCurrentDayBorder: true, 
    defaultEntryIntensity: 4,   
    intensityScaleStart: 100,  
    intensityScaleEnd: 100,   
    entries: [],    
                // (required) populated in the DataviewJS loop below
}

//DataviewJS loop
for (let page of dv.pages('"4. daily notes"').where(p => p.wakeAndSleep)) {
    //dv.span("<br>" + page.file.name) // uncomment for troubleshooting
    calendarData.entries.push({
        date: page.file.name,     
        intensity: page.wakeAndSleep,  
		color: "blue", 
	    content: await dv.span(`[](${page.file.name})`),
    })
}

renderHeatmapCalendar(this.container, calendarData)

```

# 운동 tracker

```dataviewjs
dv.span("**🏋️ Exercise 🏋️** (Green if you reached your goal of 45 minutes)")
/* optional ⏹️💤⚡⚠🧩↑↓⏳📔💾📁📝🔄📝🔀⌨️🕸️📅🔍✨ */

const calendarData = {
    year: 2022,
   
    colors: {
        green: ["#c6e48b", "#7bc96f", "#49af5d", "#2e8840", "#196127"],
    },
	defaultEntryIntensity: 4,   // (optional) defaults to 4
    intensityScaleStart: 0,    // (optional) defaults to lowest value passed to entries.intensity
    intensityScaleEnd: 100,
    entries: []
}

for(let page of dv.pages('"4. daily notes"').where(p=>p.exercise)){
    calendarData.entries.push({
        date: page.file.name,
        intensity: page.exercise,
	    color: "green", 
	    content: await dv.span(`[](${page.file.name})`),
    })
       
}

renderHeatmapCalendar(this.container, calendarData)

```


