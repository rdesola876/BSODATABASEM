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
