<p id="last-updated">Loading...</p>

<script>
async function getLastUpdated() {
    const response = await fetch("https://api.github.com/repos/Netrajit1/last-updated/commits?per_page=1");
    const commits = await response.json();
    const date = new Date(commits[0].commit.committer.date);

    document.getElementById("last-updated").innerHTML =
        "Last Updated: " +
        date.toLocaleDateString("en-IN", {
            day: "2-digit",
            month: "long",
            year: "numeric"
        });
}
getLastUpdated();
</script>
