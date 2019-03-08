<template>
    <div>
        <h4>DIVISIONS</h4>
        <table class="table table-bordered table-hover">
            <tbody>
                <div v-for="(division, key) in divisions" :key="key" class="card">
                    <draggable :id="key"
                        v-model="services" :options="{group:'services'}" @start="drag=true" 
                        @end="drag=false" @add="newDivisionService">
                        <tr>
                            <td style="width: 1%; font-weight:bold;">{{ division.code }}</td>
                            <td style="width: 1%">{{ division.name }}</td>
                            <td style="width: 1%">{{ division.countryCode }}</td>
                        </tr>
                    </draggable>
                    <table>
                        <tbody>
                            <tr class="row-aligned" v-for="(service, key) in division.services" :key="key">
                                <td> 
                                    <i class="fas fa-play element-aligned" style="font-size: 10px;" ></i>
                                    {{ service[0].name }}
                                </td>
                            </tr>
                        </tbody>
                    </table>
                </div>
            </tbody>
        </table>
    </div>
</template>

<script>
    import { eventBus } from '../src/main.js';
    import draggable from 'vuedraggable';

    export default {
        data: () => {
            return {
                services: [],
                divisions: [
                    { code: 'DD1', name: 'DHI', countryCode: '51', services: [] },
                    { code: 'DD2', name: 'DHT', countryCode: '08', services: [] },
                    { code: 'DD3', name: 'DHF', countryCode: '07', services: [] },
                    { code: 'DD4', name: 'DHP', countryCode: '09', services: [] },
                    { code: 'DD5', name: 'DHQ', countryCode: '05', services: [] }
                ]
            }
        },
        components: {
            draggable
        },
        created () {
            eventBus.$on('sendingService', serviceData => {
                console.log(serviceData);
                console.log(this.divisions);
                this.divisions[serviceData.division].services.push(serviceData.service);
            });
        },
        methods: {
            // this is called when a new service is dropped into a division
            newDivisionService: function (event) {
                console.log(event.to.id);
                eventBus.$emit('divisionSelected', event.to.id);
            }
        }
    }
</script>

<style scoped>
    .row-aligned {
        vertical-align: middle;
    }

    .element-aligned {
        padding-left: 8px;
    }
</style>

