# BSODATABASEM
<script>
const searchInput = document.getElementById("searchInput");
const cards = document.querySelectorAll("#personnelList .col");
let timeoutId;

searchInput.addEventListener("input", e => {
clearTimeout(timeoutId); // Clear any existing timeout

timeoutId = setTimeout(() => {
const search = e.target.value.toLowerCase();
cards.forEach(card => {
const text = card.innerText.toLowerCase();
card.style.display = text.includes(search) ? "" : "none";
});
}, 300); // Adjust the delay (in milliseconds) as needed
});
</script>
<script>
const searchInput = document.getElementById("searchInput");
const personnelList = document.getElementById("personnelList");
const cards = personnelList.querySelectorAll(".col");
let personnelData = [];

// Pre-process data when the page loads
document.addEventListener("DOMContentLoaded", () => {
cards.forEach(card => {
const nameElement = card.querySelector(".name"); // Assuming you have specific elements for data
const jobElement = card.querySelector(".job");
const name = nameElement ? nameElement.innerText.toLowerCase() : "";
const job = jobElement ? jobElement.innerText.toLowerCase() : "";
personnelData.push({ card, name, job });
});
});

searchInput.addEventListener("input", e => {
const search = e.target.value.toLowerCase();

personnelData.forEach(person => {
const matches = person.name.includes(search) || person.job.includes(search);
person.card.style.display = matches ? "" : "none";
});
});
</script>

`<div class="col">
<div class="name">John Doe</div>
<div class="job">Software Engineer</div>
</div>`
Then, in your JavaScript (combining with pre-indexing for better performance):
<script>
// ... (previous script with pre-indexing) ...
</script>

<script>
const searchInput = document.getElementById("searchInput");
const personnelList = document.getElementById("personnelList");
const cards = personnelList.querySelectorAll(".col");
let fuse; // Fuse.js instance
let cardData = [];

document.addEventListener("DOMContentLoaded", () => {
cardData = Array.from(cards).map(card => ({
element: card,
name: card.querySelector(".name")?.innerText || "",
job: card.querySelector(".job")?.innerText || "",
// Add other relevant data here
}));

const options = {
shouldSort: true,
keys: ["name", "job"], // Specify the keys to search within
threshold: 0.6, // Adjust for fuzzy matching sensitivity (0 = exact, 1 = broad)
};

fuse = new Fuse(cardData, options);
});

searchInput.addEventListener("input", e => {
const search = e.target.value;
const results = fuse.search(search);

// Hide all cards initially
cards.forEach(card => card.style.display = "none");

// Display the matching cards
results.forEach(result => {
result.item.element.style.display = "";
});

// If the search is empty, show all cards again
if (!search) {
cards.forEach(card => card.style.display = "");
}
});
</script>

