<template>
    <div id="app">
        <section class="section">
            <h2>Standard Dropdown</h2>
            <p>The dog you've chosen has a score of: {{dogScore}}</p>
            <dropdown 
                :data="dropdownItems" 
                :display-key="'label'" 
                :current-selection="'Please select'" 
                @update="alertDogScore($event)" />
        </section>
        
        <section class="section">
            <h2>Dropdown with Sections</h2>
            <p>The name you've chosen has a score of: {{nameScore}}</p>
            <dropdown 
                :sections="sectionedDropdownItems" 
                :display-key="'name'" 
                :current-selection="sectionedDropdownItems[1].data[2].name" 
                @update="alertNameScore($event)" />
        </section>
        
    </div>
</template>

<script>
    import Dropdown from './components/Dropdown.vue'
    
    export default {
        name: 'app',
        components: {
            'dropdown': Dropdown
        },
        data() {
            return {
                dogScore: null,
                nameScore: null,
                dropdownItems: [
                    { label: 'Corgi', value: 1000 },
                    { label: 'Australian Shepard', value: 950 },
                    { label: 'Beagle', value: 900 },
                    { label: 'Labrador', value: 750 },
                    { label: 'Goldendoodle', value: 600 }
                ],
                sectionedDropdownItems: [
                    {
                        sectionTitle: 'Girl Names',
                        data: [
                            { value: 100, name: 'Susie' },
                            { value: 200, name: 'Debbie' },
                            { value: 50, name: 'Patricia' }
                        ]
                    },
                    {
                        sectionTitle: 'Boys',
                        data: [
                            { value: 100, name: 'John' },
                            { value: 200, name: 'Steve' },
                            { value: 50, name: 'Harry' }
                        ]
                    }
                ]
            }
        },
        methods: {
            alertDogScore($event) {
                this.dogScore = $event.value;
                this.sectionDropdown__isOpen = false;
            },
            alertNameScore($event) {
                this.nameScore = $event.value;
                this.dropdown__isOpen = false;
            }
        }
    }
</script>

<style>
    .section {
        width: 100%;
        max-width: 600px;
        margin: 40px auto;
    }
    h2 {
        font-family: 'Avenir', 'Helvetica Nueue', sans-serif;
        font-size: 20px;
        margin: 20px 0;
    }
    p {
        font-family: 'Avenir', 'Helvetica Nueue', sans-serif;
        font-size: 14px;
        margin: 20px 0;
    }
</style>
