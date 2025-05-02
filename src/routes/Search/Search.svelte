

<script>
const roverOptions = [
    { value: 'all', name: 'All Rovers' },
    { value: 'perseverance', name: 'Perserverance' },
    { value: 'curiosity', name: 'Curiosity' },
    { value: 'opportunity', name: 'Opportunity' },
    { value: 'spirit', name: 'Spirit' },

];

const cameraOptions = [
    { value: 'all', name: 'All Cameras' },
    { value: 'FHAZ', name: 'Front Hazard Avoidance Camera' },
    { value: 'RHAZ', name: 'Rear Hazard Avoidance Camera' },
    { value: 'MAST', name: 'Mast Camera' },
    { value: 'CHEMCAM', name: 'Chemistry and Camera Complex' },
    { value: 'MAHLI', name: 'Mars Hand Lens imager' },

    { value: 'MARDI', name: 'Mars Descent Imager' },
    { value: 'NAVCAM', name: 'Navigation Camera ' },
    { value: 'PANCAM', name: 'Panoramic Camera' },
    { value: 'MINITES', name: 'Miniature Thermal Emission Spectrometer' },
];

let selectedRover = 'all';
let selectedCamera = 'all';
let startDate = '';
let endDate = '';

Funtion getLast7Days() {
    const today = new Date();
    const lastWeek = new Date(today);
    lastWeek.setDate(today.getDate() - 6);
    return {
        start: lastWeek.toISOString().split('T')[0],
        end: today.toISOString().split('T')[0]
    
    };
}

async function fetchPhotos() {
    let rovers = selectedRover === 'all'
        ? ['perseverance', 'curiosity', 'opportunity', 'spirit']
        : [selectedRover]
    
    if (!startDate && !endDate) {
        for (const rover of rovers) {
            let url = 
`https://api.nasa.gov/mars-photos/api/v1/rovers/${rover}/latest_photos?api_key=${import.meta.env.VITE_NASA_API_KEY}`;
            if (selectedCamera !== 'all') {
                url += `&camera=${selectedCamera}`;
            }
            const res = await fetch(url);
            const data = await res.json();
            console.log(`Here's the latest photos for ${rover}:`, data.lastest_photos);
        }
        return;
    }
    let { start, end} = { start: startDate, end: endDate };
    for (const rover of rovers) {
        let url = 
`https://api.nasa.gov/mars-photos/api/v1/rovers/${rover}/photos?api_key=${import.meta.env.VITE_NASA_API_KEY}`;
        url += `&earth_date=${end}`;
        if (selectedCamera !== 'all') {
            url += `&camera=${selectedCamera}`;
        }
        const res = await fetch(url);
        const await res.json();
        console.log(`Here are photos for ${rover} on ${end}:`, data.photos);
    }
}
</script>

<h1>Mars Rover Photo Search</h1>

<form on:submit|preventDefault={fetchPhotos}>
  <label>
    Rover:
    <select bind:value={selectedRover}>
      {#each roverOptions as rover}
        <option value={rover.value}>{rover.name}</option>
      {/each}
    </select>
  </label>
  <br />

  <label>
    Camera:
    <select bind:value={selectedCamera}>
      {#each cameraOptions as camera}
        <option value={camera.value}>{camera.name}</option>
      {/each}
    </select>
  </label>
  <br />

  <label>
    Start Date:
    <input type="date" bind:value={startDate} />
  </label>
  <br />

  <label>
    End Date:
    <input type="date" bind:value={endDate} />
  </label>
  <br />

  <button type="submit">Search</button>
</form>

<p>
  If you leave everything blank, you'll get the most recent photos from all rovers and all cameras
  (last 7 days).
</p>
