<template>
    <div>
        <div>
            <label>Patient Name:</label>
            {{name}}
        </div>
        <div>
            <label>Date of Birth:</label>
            {{dob}}
        </div>
        <div>
            <label>Health Card Number:</label>
            {{hcNum}}
        </div>
        <div>
            <label>Gender:</label>
            {{gender}}
        </div>

    </div>
</template>

<script>
    export default {
        name: 'Display',
        props: {
            name: String,
            dob: String,
            hcNum: String,
            gender:String
        }
    }
</script>