<template>
<div class="w-full h-full">
    <div class="text-2xl text-center p-2">Code Wizards API Testing</div>
    <div class="flex">
        <div class="basis-1/4 flex flex-col gap-y-2 items-center">
            <button @click="getResponse()" class="border-2 w-64 border-zinc-600 active:bg-zinc-700 hover:border-zinc-400 shadow-lg px-6 py-2">Fetch</button>
            <button @click="output = {}" class="border-2 w-64 border-zinc-600 active:bg-zinc-700 hover:border-zinc-400 shadow-lg px-6 py-2">Clear</button>
        </div>
        <div class="basis-3/4 w-96 h-full space-y-2">
            <div class="flex">
                <select name="method" id="method" v-model="reqMethod">
                    <template v-for="method in ['GET', 'POST', 'PUT', 'PATCH', 'DELETE']" :key="method">
                        <option :value="method">{{method}}</option>
                    </template>
                </select>
                <input type="text" class="w-full text-black bg-zinc-100 border-2 border-zinc-900 h-8 px-4" :value="apiUrl" :onchange="(e)=>apiUrl=e.target.value" />
            </div>
            <div class="overflow-x-auto border-2" style="max-height: 600px;">
                <pre class="text-purple-300" v-html="JSON.stringify(output, undefined, 4)" />
            </div>
        </div>
    </div>
</div>
</template>

<script>
import axios from "axios";
export default {
    name: "Frame",
    data:()=>({
        output: {},
        reqMethod: "GET",
        apiUrl:"http://localhost:8000/student"
    }),
    methods:{
        getResponse(){
            (async ()=>{
                try {
                    const out = await axios[this.reqMethod.toLowerCase()](this.apiUrl);
                    this.output = out.data;
                } catch (error) {
                    this.output = error.message;
                }
            })();
        }
    },
}
</script>