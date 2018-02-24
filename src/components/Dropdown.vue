<template>
    <div class="dropdown" :class="{ active: isOpen }" v-on-clickaway="away" @keyup.esc="close()">
        <button class="dropdown__button" tabindex="0" v-text="selectedItem[displayKey] || selectedItem" @click.stop="toggle"></button>
        <i class="dropdown__caret"></i>

        <template v-if="hasSections && isOpen">
            <div class="dropdown__section">
                <ul v-for="(section, idx) in sections"
                    :key="idx"
                    :class="{active: isOpen}"
                    class="dropdown__ul">
                <li class="dropdown__sectionTitle">
                <b>{{ section.sectionTitle }}</b>
                </li>
                <li class="dropdown__li"
                    tabindex="0"
                    :key="i"
                    v-for="(item, i) in section.data"
                    :class="{ active: selectedItem == item}"
                    v-text="displayKey === undefined ? item : item[displayKey]"
                    @click.prevent.stop="update(item)"></li>
                </ul>
            </div>
        </template>

        <template v-if="!hasSections && isOpen">
            <ul class="dropdown__ul" :class="{active: isOpen}">
                <li class="dropdown__li" 
                    tabindex="0" 
                    :key="i" v-for="(item, i) in data" 
                    :class="{ active: selectedItem == item.id}" 
                    v-text="displayKey === undefined ? item : item[displayKey]" 
                    @click.prevent.stop="update(item)"></li>
            </ul>
        </template>
</div>
</template>

<script>
    import {
        mixin as clickaway
    } from "vue-clickaway";
    
    export default {
        name: "dropdown",
        mixins: [clickaway],
        props: {
            data: {
                type: Array,
                default: () => ["No Items"]
            },
            displayKey: {
                type: String
            },
            currentSelection: {
                type: [Object, String]
            },
            sections: {
                type: Array,
                default: () => []
            },
            sectionTitle: {
                type: String,
                required: false
            }
        },
        data() {
            return {
                isOpen: false,
                selectedItem: this.currentSelection
            };
        },
        computed: {
            hasSections() {
                return this.sections.length > 0;
            }
        },
        methods: {
            open() {
                this.isOpen = true;
            },
            close() {
                this.isOpen = false;
            },
            toggle($event) {
                this.isOpen ? this.close() : this.open();
            },
            away($event) {
                if (this.isOpen) this.close();
            },
    
            update(item) {
                this.selectedItem = item;
                this.$emit("update", this.selectedItem);
                this.close();
            }
        }
    };
</script>

<style lang="scss">
    $gray: #999;
    $darker-gray: #555;

    .dropdown {
        box-sizing: border-box;
        position: relative;
        border: 1px solid #999;
        border-radius: 4px;
        cursor: pointer;
        font-family: 'Avenir', 'Helvetica Nueue', sans-serif;
        display: block;
    }
    
    .dropdown__button {
        border: 0 none;
        padding: 8px 25px 8px 12px;
        font-size: 15px;
        line-height: 1.53;
        color: #555;
        background-color: transparent;
        width: 100%;
        white-space: nowrap;
        text-align: left;
        cursor: pointer;
        box-sizing: border-box;
    }
    
    .dropdown__caret {
        font-size: 10px;
        color: #555;
        position: absolute;
        top: 50%;
        right: 10px;
        pointer-events: none;
        display: inline-block;
        width: 0;
        height: 0;
        margin-left: 2px;
        vertical-align: middle;
        border-top: 4px dashed;
        border-top: 4px solid\9;
        border-right: 4px solid transparent;
        border-left: 4px solid transparent;
    }
    
    .dropdown__ul {
        padding: 0;
        margin: 8px 0 0 0;
        list-style-type: none;
        background-color: #fff;
        box-sizing: border-box;
        box-shadow: 0 0 10px rgba(0,0,0,0.25);
        position: absolute;
        top: 100%;
        display: block;
        width: 100%;
        z-index: 10;
    }
    
    .dropdown__section {
        margin: 8px 0 0 0;
        background-color: #fff;
        box-shadow: 0 0 10px rgba(0,0,0,0.25);
        box-sizing: border-box;
        position: absolute;
        top: 100%;
        left: 0;
        width: 100%;
        z-index: 10;
        .dropdown__ul {
            position: static;
            box-shadow: 0 0 0 0;
            padding: 0 0 20px;
            list-style-type: none;
            &+.dropdown__ul {
                margin-top: 0;
                padding-top: 20px;    
                border-top: 1px solid #eee;
            }
        }
        .dropdown__li {
            font-weight: normal;
            padding: 3px 20px;
        }
    }
    
    .dropdown__sectionTitle {
        padding: 3px 20px;
        margin-bottom: 5px;
    }
    
    .dropdown__li {
        padding: 8px 10px;
        text-align: left;
        font-size: 14px;
        color: #555;
        &.active {
            font-weight: bold;
        }
    }
</style>
