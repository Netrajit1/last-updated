<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Last Updated</title>

    <style>
        body{
            font-family: Arial, sans-serif;
            background:#ffffff;
            margin:20px;
        }

        #last-updated{
            font-size:16px;
            color:#666;
            font-weight:500;
        }
    </style>
</head>
<body>

<p id="last-updated">Last Updated: Loading...</p>

<script>
async function getLastUpdated() {

    const owner = "Netrajit1";
    const repo = "last-updated";

    const url = `https://api.github.com/repos/${owner}/${repo}/commits?per_page=1`;

    try {

        const response = await fetch(url);

        if(!response.ok){
            throw new Error("Unable to fetch data");
        }

        const commits = await response.json();

        const lastCommit = new Date(commits[0].commit.committer.date);

        const formattedDate = lastCommit.toLocaleDateString("en-IN",{
            day:"2-digit",
            month:"long",
            year:"numeric"
        });

        document.getElementById("last-updated").innerHTML =
        "Last Updated: " + formattedDate;

    }
    catch(error){

        document.getElementById("last-updated").innerHTML =
        "Last Updated: Not Available";

        console.error(error);

    }

}

getLastUpdated();
</script>

</body>
</html>
