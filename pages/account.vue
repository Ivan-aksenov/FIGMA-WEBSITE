<script setup >

    //for form
        import { ref } from 'vue'



    const popup = ref(true);
    function popmodal(index){
        popup.value = false
        selectedEmployeeIndex.value=index

        newEmployee.value ={
            photoURL: employees.value[selectedEmployeeIndex.value]['photoURL'],
            firstName: employees.value[selectedEmployeeIndex.value]['firstName'],
            middleName: employees.value[selectedEmployeeIndex.value]['middleName'],
            lastName: employees.value[selectedEmployeeIndex.value]['lastName'],
            email: employees.value[selectedEmployeeIndex.value]['email'],
            department: employees.value[selectedEmployeeIndex.value]['department'],
            idNo: employees.value[selectedEmployeeIndex.value]['idNo'],
            active: employees.value[selectedEmployeeIndex.value]['Active'],
            deactivated: employees.value[selectedEmployeeIndex.value]['Deactive'],
        };
    }

    const resetpop = ref(true);
    function respop(){
        resetpop.value = false
    }
    const deletepop= ref(true);
    function delpop(){
        deletepop.value = false
    }
    
            
    const isModalHidden = ref(true);
    function openModal(){
        isModalHidden.value = false
    }

    const employees = ref([]);
    const newEmployee = ref({
        photoURL: '',
        firstName: '',
        middleName: '',
        lastName: '',
        email: '',
        department: '',
        idNo: '',
        active: false,
        deactivated: false,
    });

    data:{
        errors:[]
        photoURL:null;
        firstName:null;
        middleName:null;
        lastName:null;
        email:null;
        department:null;
        idNo:null;
        active: false;
        deactivated: false;
    }


    const isAddButtonDisabled = computed(() => {   const { firstName, lastName, email, department, idNo } = newEmployee.value;   return !(firstName && lastName && email && department && idNo); });

    function addEmployee(){

        employees.value.push({
            photoURL: newEmployee.value.photoURL,
            firstName: newEmployee.value.firstName,
            middleName: newEmployee.value.middleName,
            lastName: newEmployee.value.lastName,
            email: newEmployee.value.email,
            department: newEmployee.value.department,
            idNo: newEmployee.value.idNo,
            active: newEmployee.value.active,
            deactivated: newEmployee.value.deactivated,
        });

        newEmployee.value ={
            photoURL: '',
            firstName: '',
            middleName: '',
            lastName: '',
            email: '',
            department: '',
            idNo: '',
            active: false,
            deactivated: false,
        };

    }

    const formattedDate = new Date().toLocaleDateString(undefined, {
    year: 'numeric',
    month: 'short',
    day: 'numeric'
    });

    const selectedEmployeeIndex = ref(null);
    function showDetails(index) {
        selectedEmployeeIndex.value = index;
    }

    function hideDetails() {
        selectedEmployeeIndex.value = null;
    }


    function deleteemp(){

  employees.value.splice(selectedEmployeeIndex.value, 1);

        newEmployee.value ={
            photoURL: '',
            firstName: '',
            middleName: '',
            lastName: '',
            email: '',
            department: '',
            idNo: '',
            active: false,
            deactivated: false
        }
    }

    function Updatefunc(){
        employees.value = {
            photoURL: '',
            firstName: '',
            middleName: '',
            lastName: '',
            email: '',
            department: '',
            idNo: '',
            active: false,
            deactivated: false,
        }
    }

    function resetfunc(){
        newEmployee.value ={
            photoURL: '',
            firstName: '',
            middleName: '',
            lastName: '',
            email: '',
            department: '',
            idNo: '',
            active: false,
            deactivated: false,
}
    }



</script>

<template>
    <!--Logo-->
    <!--
    <div class="ox-content">
        <img src="~/assets/Logo.svg" >
    </div>
-->
    <nav class="hidden p-5 md:flex md:items-center md:justify-between border">
        <div class="font-plus-jakarta-sans">
            <span class="cursor-pointer">
                <img class="h-10 inline" src="~/assets/Logo.svg">
            </span>
        </div>
        <ul class="md:flex md:items-center">
            <li class="mx-4 ">
                <NuxtLink to="/index">
                    <a href="#" class=" ">HOME</a>
                </NuxtLink>
            </li>
            <li class="mx-4">
                <NuxtLink to="/account">
                    <a href="#" class="border-b-4 border-red-500 mt-5">ACCOUNTS</a>
                </NuxtLink>
            </li>
            <li class="mx-4">
                <a href="#" class="">SALES</a>
            </li>
            <li class="mx-2 cursor-pointer">
                <img src="~/assets/bell.svg" >
            </li>
            <li class="mx-2 cursor-pointer">
                <img src="~/assets/message.svg" >
            </li>
            <li class="mx-2 cursor-pointer">
                <img src="~/assets/user.svg" >
            </li>
        </ul>
    </nav>
    <!--Modal-->
                        <div class="flex justify-start p-5 border">
                                <div class="flex space-x-3" >
                                    <div class="relative flex flex-wrap">
                                        <form action="">
                                            <input type="text"
                                            name="search"
                                            placeholder="Search" 
                                            autocomplete="off"
                                            class="hidden md:block ml-9 px-10 py-2 placeholder-gray-500 text-black rounded border-none ring-2 ring-gray-300 focus:ring-gray-500 focus:ring-2">
                                        </form>
                                        <img class="absolute pt-3 pl-1 mr-5 top-0 right-0" src="~/assets/Vector.svg">
                                    </div>
                                    
                                    <div class="relative">
                                        <!--Department-->
                                        <div>
                                            <img class="absolute border-8 border-red-500 rounded-l-lg bg-red-500" src="~/assets/Group.svg">
                                            <form action="" class="mr-28">
                                                <input type="text"
                                                name="Department"
                                                placeholder="Department"
                                                autocomplete="off"
                                                class="border hidden md:block px-10  py-2 placeholder-gray-500 text-black rounded border-none ring-2 ring-gray-300 focus:ring-gray-500 focus:ring-2">
                                            </form>

                                            
                                        </div>
                                    </div>
                                    <!-- Modal Trigger Button -->
                                    <div>
                                                <a href="#" class="absolute right-20 text-m ml-20 text-start hidden md:block px-10 p-2 text-white bg-red-500 rounded baseline" @click="openModal()" >+ New</a>
                                            </div>
                                    

                                    </div>
                            </div>
                            <div :class="{ 'hidden': isModalHidden }" class=" inset-0 z-50 overflow-auto " id="modal">
                                                <div class="flex items-center justify-center min-h-screen">
                                                    <div class="bg-white p-1 rounded shadow-md ">
                                                        <!-- MODAL FORM -->
                                                        <div class="flex p-1 space-x-1">
                                                            <!-- Left side with Upload button -->
                                                            <div class="w-1/4 flex flex-col">
                                                                <label class=" font-semibold py-2 px-4 rounded cursor-pointer block text-center text-white-500 underline decoration-1 visited:text-sky-500">
                                                                    <div class="flex flex-col items-center">
                                                                        <div class="flex space-x-2 border-2 border-gray-500 p-10 border-dashed">
                                                                            <img src="~/assets/upload.svg" class="w-10 h-10 " alt="Upload Icon">
                                                                        </div>
                                                                        <span class="mt-2">Upload File</span>
                                                                    </div>
                                                                    <input type="file" class="hidden">
                                                                </label>
                                                            </div>

                                        <!-- Right side with form fields -->
                                        <div class="w-3/4 ">
                                                    <div class="space-y-4">
                                                        <!-- Name fields -->
                                                        <div class="grid grid-cols-4 gap-10">
                                                            <input type="text" class="p-2 border rounded" id="fName" placeholder="First Name" v-model="newEmployee.firstName">
                                                            <input type="text" class="p-2 border rounded" id="mname" placeholder="Middle Name" v-model="newEmployee.middleName" required>
                                                            <input type="text" class="p-2 border rounded" id="lname" placeholder="Last Name" v-model="newEmployee.lastName" required>
                                                            <button id="Add"  @click="addEmployee" :disabled="isAddButtonDisabled" class="bg-green-500 hover:bg-green-600 text-white font-semibold py-4 rounded">
                                                                Add
                                                            </button>
                                                        </div>

                                                        <!-- Email, Department, ID No. -->
                                                        <div class="grid grid-cols-4 gap-10 items-center">
                                                            <input type="email" class="p-2 border rounded" id="email" placeholder="Email" v-model="newEmployee.email" required>
                                                            <input type="text" class="p-2 border rounded" id="department" placeholder="Department" v-model="newEmployee.department" required>
                                                            <input type="text" class="p-2 border rounded" id="ID" placeholder="ID No." v-model="newEmployee.idNo" required>
                                                            <button @click=" isModalHidden = true " class="bg-gray-500 hover:bg-gray-400 text-white font-semibold py-4 rounded">
                                                                Cancel
                                                            </button>
                                                </div>
                                                

                                                <!-- Checkboxes for Active and Deactive -->
                                                <div class="flex space-x-4">
                                                    <label class="flex items-center" >
                                                        <input type="checkbox" class="form-checkbox h-4 w-4 text-indigo-600" id="active-checkbox"  for="active-checkbox" v-model="newEmployee.active">
                                                        <span class="ml-2">Active</span>
                                                    </label>
                                                    <label class="flex items-center" for="deactivated-checkbox">
                                                        <input type="checkbox" class="form-checkbox h-4 w-4 text-indigo-600" id="deactivated-checkbox" for="deactive-checkbox" v-model="newEmployee.deactivated">
                                                        <span class="ml-2">Deactive</span>
                                                    </label>
                                                </div>
                                            </div>
                                            <div>

                                            </div>
                                        </div>  
                                    </div>
                                </div>
                            </div>
                        </div>
                                        
                        <div class="flex justify-center pt-10 ">
                                        <img class="p-2" src="~/assets/Need something done_.svg">
                                        <img src="~/assets/Rectangle 22.svg">
                                    </div>

                                    <!--HEAD-->
                                    <div class="flex justify-end">             
                                        <table class=" w-[100%]">
                                            <thead>
                                                <tr >
                                                    <th class="py-2 px-1 font-light text-gray-500 text-left flex items-center">
                                                        <label class="inline-flex items-center">
                                                            <input type="checkbox" class="form-checkbox h-4 w-4 text-indigo-600">
                                                            <span class="ml-2">File Name/ID No.</span>
                                                        </label>
                                                    </th>
                                                    
                                                    <th class="py-2 px-3 font-light text-gray-500 text-left">Date</th>
                                                    <th class="py-2 px-3 font-light text-gray-500 text-left">Email</th>
                                                    <th class="py-2 px-3 font-light text-gray-500 text-left">Department</th>
                                                    <th class="py-2 px-3 font-light text-gray-500 text-left" >Active</th>
                                                </tr>
                                            </thead>
                                            <tbody class="border-y-2 pxs-5 bg-gray-100">
                                                <tr v-for="(employee, index) in employees" :key="index" @click="popmodal(index)">
                                                    <td class = "py-2 px-1" > 
                                                    <div class = "text-[#101828]"><input type="checkbox" class="form-checkbox h-4 w-4 text-indigo-600" id="deactivated-checkbox"> {{ employee.firstName }} {{ employee.middleName }} {{ employee.lastName }} </div>
                                                    <div class = "text-[#667085]">{{  employee.idNo }}</div></td>
                                                    <td class = "text-[#667085] py-2 px-3">{{ formattedDate }}</td>
                                                    <td class = "text-[#667085] py-2 px-3">{{ employee.email }}</td>
                                                    <td class = "text-[#667085] py-2 px-3">{{ employee.department }}</td>
                                                    <td class="text-[#667085] py-2 px-3" :style = "{'color' : employee.active ? 'green' : (employee.deactivated ? 'red' : '')}">
                                                        {{ employee.active ? 'Active' : (employee.deactivated ? 'Deactivated':'')}} </td><img src="~/assets/Dropdown.svg">  
                                                </tr>
                                            </tbody>
                                        </table>


                                <div class="bg-white rounded mx-1 cursor-pointer " >
                                            <!--MODAL CONTENT-->
                                    <div :class="{ 'hidden': popup }" class=" inset-0 z-50 " id="modal">
                                        <div class="flex items-center justify-end space-x-5 ">
                                            <div >

                                                <!--DELETE -->
                                                <div class="flex space-x-2 justify-end">
                                                    <button @click="respop"><img src="~/assets/Group 10.svg"></button>
                                                    <div :class="{ 'hidden': deletepop }" class="fixed inset-0 bg-gray-4 flex items-center justify-center z-50">
                                                        <div class="bg-white p-6 rounded shadow-md w-96 border-t-8 border-red-400">
                                                            <div class="flex flex-box">
                                                            <img src="~/assets/trash bin.svg"><h2 class="text-lg font-semibold mb-4 pl-5 pt-5">Delete Account</h2>
                                                        </div>
                                                            <p class="text-gray-700 mb-6">You'll permanently delete all the data, messages, photos and important information.</p>
                                                            <div class="flex justify-center">
                                                                <button @click=" deletepop = true " class="px-4 py-2 bg-gray-400 text-gray-300 hover:bg-gray-200 rounded-md mr-2">
                                                                    Cancel
                                                                </button>
                                                                <button @click="deleteemp" class="px-4 py-2 bg-red-500 text-white rounded-md">Delete</button>
                                                            </div>
                                                        </div>
                                                    </div>
                                                </div>
                                            </div>        

                                            <!--RESET-->
                                                    <button><img src="~/assets/Group 11.svg"></button>
                                                    <div :class="{ 'hidden': resetpop }" class="fixed inset-0 bg-gray-4 flex items-center justify-center z-50">
                                                        <div class="bg-white p-6 rounded shadow-md w-96 border-t-8 border-yellow-400">
                                                            <div class="flex flex-box">
                                                            <img src="~/assets/Reboot.svg"><h2 class="text-lg font-semibold mb-4 pl-5 pt-5">Reset Profile</h2>
                                                        </div>
                                                            <p class="text-gray-700 mb-6">Are you sure you want to reset this profile? If you reset this profile, you will permanently lose all the important data.</p>
                                                            <div class="flex justify-center">
                                                                <button @click=" resetpop = true " class="px-4 py-2 bg-gray-400 text-gray-300 hover:bg-gray-200 rounded-md mr-2">
                                                                    Cancel<!--INSERT RESET FUNCTION!!-->
                                                                </button>
                                                                <button @click="resetfunc" class="px-4 py-2 bg-yellow-400 text-white rounded-md" type="reset" value="reset">Reset</button>
                                                            </div>
                                                        </div>
                                                    </div>
                                                    <button @click="delpop"><img src="~/assets/Group 15.svg"></button>
                                                </div>

                                                <!-- MODAL FORM -->
                                                <div class="flex flex-col p-4 space-x-2">
                                                    <!-- Left side with Upload button -->
                                                    <div class="w-1/4 flex flex-col">
                                                        <label class="font-semibold py-2 px-4 rounded cursor-pointer block text-center text-white-500 underline decoration-1 visited:text-sky-500">
                                                            <div class="flex flex-col items-center">
                                                                <div class="flex space-x-2 border-2 border-gray-500 p-2 border-dashed rounded">
                                                                    <img src="~/assets/upload.svg" class="w-10 h-10" alt="Upload Icon">
                                                                </div>
                                                                <span class="">Upload File</span>
                                                            </div>
                                                            <input type="file" class="hidden">
                                                        </label>
                                                    </div>

                                                <!--FOR RESET-->
                                                <!-- Right side with form fields -->
                                                <div class="min-w-full">
                                                    <div class="space-y-2">
                                                        <!-- Name fields -->
                                                        <div class="grid grid-cols-3 gap-2">
                                                            <input type="text" class="p-2 border rounded" id="fName" placeholder="First Name" v-model="newEmployee.firstName" required>
                                                            <input type="text" class="p-2 border rounded" id="mname" placeholder="Middle Name" v-model="newEmployee.middleName" required>
                                                            <input type="text" class="p-2 border rounded" id="lname" placeholder="Last Name" v-model="newEmployee.lastName" required>
                                                        </div>

                                                        <!-- Email, Department, ID No. -->
                                                        <div class="grid grid-cols-3 gap-2 items-center">
                                                            <input type="email" class="p-2 border rounded" id="email" placeholder="Email" v-model="newEmployee.email" required>
                                                            <input type="text" class="p-2 border rounded" id="department" placeholder="Department" v-model="newEmployee.department" required>
                                                            <input type="text" class="p-2 border rounded" id="ID" placeholder="ID No." v-model="newEmployee.idNo" required>
                                                        </div>

                                                        <!-- Buttons -->
                                                        <div class="flex space-x-2">
                                                            <button @click="" :disabled="isAddButtonDisabled" class="bg-green-500 hover:bg-green-600 text-white font-semibold py-2 px-4 rounded">
                                                                Update
                                                            </button>
                                                            <button @click="popup = true" class="bg-gray-500 hover:bg-gray-400 text-white font-semibold py-2 px-4 rounded">
                                                                Cancel
                                                            </button>
                                                        </div>

                                                        <!-- Checkboxes for Active and Deactive -->
                                                        <div class="flex space-x-2">
                                                            <label class="flex items-center">
                                                                <input type="checkbox" class="form-checkbox h-4 w-4 text-indigo-600" id="active-checkbox" for="active-checkbox" v-model="newEmployee.active">
                                                                <span class="ml-2">active</span>
                                                            </label>
                                                            <label class="flex items-center" for="deactivated-checkbox">
                                                                <input type="checkbox" class="form-checkbox h-4 w-4 text-indigo-600" id="deactivated-checkbox" for="deactive-checkbox" v-model="newEmployee.deactivated">
                                                                <span class="ml-2">Deactive</span>
                                                            </label>
                                                        </div>
                                                    </div>  
                                                </div>
                                            </div>
                                        </div>
                                    </div>
                                </div>    
    <!--Table-->
    
    <!--DATA SHEET-->
    
  
 

</template>
