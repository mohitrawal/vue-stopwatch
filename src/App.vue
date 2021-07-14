<template>
    <div id="app">
        <div class="container">
            <div class="flex flex-col text-center">
                <div>
                    <h1 class="font-bold m-6">My Application</h1>
                </div>
            </div>
            <div class="grid grid-cols-6 gap-4">
                <div class="col-start-2 col-span-4">
                    <div class="mt-10 ml-80 w-41 h-56">
                        <div class="border-4 border-red-500 rounded-full h-40 w-40 flex items-center justify-center shadow-xl bg-gradient-to-r from-yellow-400 via-red-500 to-pink-500" @click="startStopFunction">
                            <div class="text-2xl">
                                {{formattedMM}}:{{formattedSS}}:{{formattedMS}}
                            </div>
                        </div>
                        <p class='mt-2 text-sm italic text-gray-400'>Click on the Circle Start/Pause</p>
                    </div>
                    <div class="grid grid-cols-6">
                        <div class="col-start-3 col-span-5 mt-1 ml-20">
                            <button class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded-full" @click="resetTimer">
                                Reset
                            </button>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: 'App',
    data: function () {
        return {
            startCounter: 0,
            formattedMM:'00',
            formattedSS:'00',
            formattedMS:'00',
            timerInterval:0,
            elapsedTime:0
        }
    },
    methods: {
        timeFormat(time) {
            let diffInHrs = time / 3600000;
            let hh = Math.floor(diffInHrs);
            let diffInMin = (diffInHrs - hh) * 60;
            let mm = Math.floor(diffInMin);

            let diffInSec = (diffInMin - mm) * 60;
            let ss = Math.floor(diffInSec);

            let diffInMs = (diffInSec - ss) * 100;
            let ms = Math.floor(diffInMs);
            this.formattedMM = mm.toString().padStart(2, "0");
            this.formattedSS = ss.toString().padStart(2, "0");
            this.formattedMS = ms.toString().padStart(2, "0");
        },
        startStopFunction () {
            if(this.startCounter === 1) {
                this.clearInterval();
                return;
            }
            this.startCounter = 1;

            let startTime = Date.now() - this.elapsedTime;
            let thisVal = this;
            this.timerInterval = setInterval(() => {
                thisVal.elapsedTime = Date.now() - startTime;
                thisVal.timeFormat(thisVal.elapsedTime);
            },10)
        },
        resetTimer() {
            clearInterval(this.timerInterval);
            this.formattedMM = this.formattedSS = this.formattedMS = "00";
            this.startCounter = 0;
            this.elapsedTime = 0;
        },
        clearInterval() {
            clearInterval(this.timerInterval);
            this.startCounter = 0;
        }
    }
}
</script>

<style>
</style>
