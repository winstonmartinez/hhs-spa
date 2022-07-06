<template>
    <div>
        <div>
            <h3>Patient Name:</h3>
            {{name}}
        </div>
        <div>
            <h3>Date of Birth:</h3>
            {{dob}}
        </div>
        <div>
            <h3>Health Card Number:</h3>
            {{hcNum}}
        </div>
        <div>
            <h3>Gender:</h3>
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