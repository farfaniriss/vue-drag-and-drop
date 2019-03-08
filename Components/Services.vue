<template>
    <div>
        <h4>SERVICES</h4>
        <table class="table table-bordered table-hover">
            <tbody>
                    <draggable v-for="(service, key) in services" :key="key" :id="key" v-model="services" 
                    :options="{group: { name:'services', pull:'clone', put:'false'}}" @start="drag=true" 
                        @end="drag=false" :move="chooseService">
                        <tr>
                            <td style="width: 1%">{{ service.code }}</td>
                            <td style="width: 1%">{{ service.name }}</td>
                            <td style="width: 1%">{{ service.description }}</td>
                        </tr>
                    </draggable>
            </tbody>
        </table>
        <!-- <v-container grid-list-md>
            <v-layout row wrap>
                <v-flex md6 v-for="(service, key) in services">
                    <draggable :id="key" v-model="services" :options="{group: { name:'services', pull:'clone', put:'false'}}" @start="drag=true" 
                        @end="drag=false" :move="chooseService">
                        <v-card class="ma-2 pa-2">
                        <v-card-title>
                            <div class="headline">{{ service.name }}</div>
                             CODE: <span> {{ service.code }}</span>
                             DESCRIPTION: <span> {{ service.description }}</span>
                        </v-card-title>
                        </v-card>
                    </draggable>
                </v-flex>
            </v-layout>
        </v-container> -->
    </div>
</template>

<script>
    import { eventBus } from '../src/main.js';
    import draggable from 'vuedraggable';

    export default {
        data: () => {
            return {
                services: [
                    { id: 0, code: 'S_0_1', name: 'Express service', description: 'Description 01' },
                    { id: 1, code: 'S_0_2', name: 'Standard service', description: 'Description 02' },
                    { id: 2, code: 'S_0_3', name: 'Another service', description: 'Description 03' },
                    { id: 3, code: 'S_0_4', name: 'Random service', description: 'Description 04' },
                    { id: 4, code: 'S_0_5', name: 'Awesome service', description: 'Description 05' },
                    { id: 5, code: 'S_0_6', name: 'Wonderful service', description: 'Description 06' },
                    { id: 6, code: 'S_0_7', name: 'Useless service', description: 'Description 07' },
                    { id: 7, code: 'S_0_8', name: 'Do not buy me service', description: 'Description 08' }
                ],
                targetService: '',
                targetDivision: ''
            }
        },
        components: {
            draggable
        },
        created () {
            eventBus.$on('divisionSelected', division => {
                
                this.targetDivision = division;
                this.sendServiceData(this.targetService);
            });
        },
        methods: {
            // this starts the service drag and drop process
            chooseService: function (event) {
                this.targetService = event.from.id;
            },
            sendServiceData: function (id) {
                // console.log('id ' + id)
                var myService = this.services.filter(function (service) {
                    return service.id == id;
                });
                var serviceData = {
                    division: this.targetDivision,
                    service: myService
                }
                eventBus.$emit('sendingService', serviceData);
            }
        }
    }
</script>

<style>


</style>
