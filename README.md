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
