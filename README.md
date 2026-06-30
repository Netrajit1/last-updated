async function getLastUpdated() {
    const owner = "Netrajit1";
    const repo = "last-updated";

    const apiUrl = `https://api.github.com/repos/${owner}/${repo}/commits?per_page=1`;

    try {
        const response = await fetch(apiUrl);

        if (!response.ok) {
            throw new Error("GitHub API Error");
        }

        const data = await response.json();

        const lastCommitDate = new Date(data[0].commit.committer.date);

        const formattedDate = lastCommitDate.toLocaleDateString("en-IN", {
            day: "2-digit",
            month: "long",
            year: "numeric"
        });

        document.getElementById("last-updated").textContent =
            `Last Updated: ${formattedDate}`;

    } catch (error) {
        console.error(error);
        document.getElementById("last-updated").textContent =
            "Last Updated: Not Available";
    }
}

document.addEventListener("DOMContentLoaded", getLastUpdated);
