{#if !reviewing}
    <button class="reviewButton" on:click={toggleReview}> Add Review </button>
{:else}
    <form class="reviewForm">
        <p>Fill out the following fields</p>
        <input type="text" name="fname" placeholder="Your First Name" bind:value={fname}>
        <input type="text" name="lname" placeholder="Your Last Name" bind:value={lname}>
        <input type="text" name="Hospital" placeholder="Hospital Name" bind:value={hospital}>
        <input type="text" name="Procedure" placeholder="Services"  bind:value={procedure}>
        <input type="text" name="Doctor" placeholder="Doctor's Name"  bind:value={doctor}>
        <input type="text" name="Specialization" placeholder="Doctor's Specialization"  bind:value={special}>
        <label for="cost">Enter the cost of the procedure: </label>
        <input type="number" name="Cost" placeholder="Cost"  id ="cost" bind:value={cost}>
        <button class="formButton" on:click={reviewed}> Done </button>
        <span class="closeForm" on:click={toggleReview}>&times;</span>
    </form>
{/if}
{#if alertInput}
    <div class="alert" id="alert">
        <span class="closebtn" on:click={toggleAlert}>&times;</span>
        Fields were incorrectly filled out.
    </div>
{/if}


<script>
    let lname = "";
    let fname = "";
    let hospital = "";
    let cost = -1;
    let procedure = "";
    let doctor = "";
    let special = "";
    let reviewing = false;
    let alertInput = false;
    function toggleReview(){
        reviewing = !reviewing;
        alertInput = false;
    }
    function toggleAlert(){
        alertInput = !alertInput;
    }
    function reviewed(event){
        event.preventDefault();
        if( cost <= 0 || lname == "" || fname == "" || hospital == "" || procedure == "" || doctor == "" || special == ""){
            alertInput = true;
        }
        const response = fetch("http://localhost:7878/review", {
            method: 'POST',
            headers: {
            'Content-Type': 'application/json'            
            },
            body: JSON.stringify({"first_name" : fname, "last_name": lname , "hospital_name" : hospital, "doctor_name" : doctor, "doctor_type" : special, "service_rendered" : procedure, "service_cost" : cost})
        });
        response.then(function(processedResponse){
            if (processedResponse.ok) {
                alert("Review Added");
                reviewing = !reviewing;
            }
        }).catch(e => {
            throw new Error(`HTTP error! status: ${e.status}`);
        });
    }
</script>

<style>
    .reviewButton{
		color: #161615;
		text-transform: uppercase;
		font-size: 30px;
		font-weight: 100;
        background: linear-gradient(rgba(196, 102, 0, 0.6),rgb(103,46,46));
        opacity: 1;
        border: 6px solid black;
	}
    
    .formButton{
		color: #161615;
		text-transform: uppercase;
		font-size: 4em;
		font-weight: 100;
        background: linear-gradient(rgba(196, 102, 0, 0.6),rgb(103,46,46));
        opacity: 1;
        border: 6px solid black; 
	}

    .reviewForm { 
        display: block;
        border: 6px solid black; 
        padding: 2em;
        width: 400px;
        text-align: center;
        background: rgb(103,46,46, 0.8);
        position: fixed;
        top:50%;
        left:50%;
        opacity: 1;
        transform: translate(-50%,-50%);
        -webkit-transform: translate(-50%,-50%)
    }

    .alert {
        padding: 20px;
        background-color: #f44336;
        color: white;
        margin-bottom: 15px;
        opacity: 1;
        transition: opacity 0.6s;
    }

    .closebtn {
        margin-left: 15px;
        color: white;
        opacity: 1;
        font-weight: bold;
        font-size: 22px;
        line-height: 20px;
        cursor: pointer;
        transition: 0.3s;
    }

    .closebtn:hover {
        color: black;
    }
    .closeForm{
        margin-left: 15px;
        color: #f44336;
        font-weight: bold;
        font-size: 22px;
        line-height: 20px;
        cursor: pointer;
        transition: 0.3s;
        position: absolute;
        right: 32px;
        top: 32px;
        width: 32px;
        height: 32px;
        opacity: 0.3;
    }
    .closeForm:hover{
        color: black
    }
    label{
        display:inline-block;
        font-size: 16px;
        text-align: center;
    }
    
</style>
