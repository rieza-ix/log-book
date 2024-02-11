<template>
    <div class="md:flex gap-4 p-4 md:max-h-screen">
        <!-- login form data -->
        <div class="md:w-[50%] md:mb-0 mb-4">
            <form class="bg-white shadow-md py-8 px-12 m-auto" @submit.prevent="handleSubmit">
                <h1 class="title">Login Form</h1>
                <div class="grid grid-cols-2 gap-8">
                    <div>
                        <label>Last Name:</label>
                        <input type="text" v-model="lastName">
                    </div>
                    <div>
                        <label>First Name:</label>
                        <input type="text" v-model="firstName">
                    </div>
                </div>

                <label>Address:</label>
                <input type="text" v-model="address">

                <div class="grid grid-cols-2 gap-8">
                    <div>
                        <label>Date:</label>
                        <input type="date" v-model="date">
                    </div>
                    <div>
                        <label>Time:</label>
                        <input type="time" v-model="time">
                    </div>
                </div>

                <label>Purpose:</label>
                <select v-model="purpose">
                    <option value=""></option>
                    <option value="Book Appointment">Book Appointment</option>
                    <option value="Walk-in">Walk-in</option>
                    <option value="Work">Work (Staff)</option>
                    <option value="Scheduled Appointment">Scheduled Appointment</option>
                </select>

                <button type="submit" class="btn">Finish</button>
            </form>
        </div>

        <!-- log book (table) -->
        <div class="w-[100%]">
            <div class=" relative overflow-x-auto bg-white shadow-md py-8 px-12 m-auto h-full ">
                <h1 class="title">Log Book</h1>
                <table>
                    <thead>
                        <tr>
                            <th>Last Name</th>
                            <th>First Name</th>
                            <th>Address</th>
                            <th>Date</th>
                            <th>Time</th>
                            <th>Purpose</th>
                        </tr>
                    </thead>
                    <tbody class="min-h-min overflow-y-auto">
                        <tr v-for="formDataEntry in formDataList" :key="formDataEntry.firstName">
                            <td>{{ formDataEntry.lastName }}</td>
                            <td>{{ formDataEntry.firstName }}</td>
                            <td>{{ formDataEntry.address }}</td>
                            <td>{{ formDataEntry.date }}</td>
                            <td>{{ formDataEntry.time }}</td>
                            <td>{{ formDataEntry.purpose }}</td>
                        </tr>
                    </tbody>
                </table>
            </div>
        </div>
    </div>
</template>
  
<script setup>
import { ref } from 'vue';

// use ref to make the variable values reactive
const lastName = ref('');
const firstName = ref('');
const address = ref('');
const date = ref(null);
const time = ref(null);
const purpose = ref('');

// initialize a reference array list to store the data from the form and to access it in the table
const formDataList = ref([]);
const formData = [lastName, firstName, address, date, time, purpose];

// log the data entered from the form to the DOM and add it to the table
const handleSubmit = () => {
    // get the data from the form
    const formDataEntry = {
        lastName: lastName.value,
        firstName: firstName.value,
        address: address.value,
        date: date.value,
        time: time.value,
        purpose: purpose.value
    };

    // push the data into the array to display to access it in the table
    formDataList.value.push(formDataEntry);

    // Clear the form fields
    lastName.value = '';
    firstName.value = '';
    address.value = '';
    date.value = null;
    time.value = null;
    purpose.value = '';

    console.log('Form submitted:', formDataEntry);
};
</script>
  