<template>
    <TooltipsRectangular class="d-flex justify-content-start align-items-end ms-4 mt-2" :toolTipState="toolTip" :toolTipText="'Filtros para Organização dos Itens'"/>
    <div class="dropdown">
        <button @mouseover="toolTip = true" @mouseout="toolTip = false" @focusin="colorFocus" @focusout="colorUnfocus" class="dropdown-principal filter-btn action-btn d-flex btn btn-outline-ligth text-dark-emphasis mx-1 px-2" data-bs-toggle="dropdown" data-bs-offset="0,2" data-bs-auto-close="inside" aria-expanded="false">
            Filtro
            <IconsFilter class="mx-1" width="1.5em" height="1.5em"/>
        </button>
        <ul class="dropdown-menu large-menu">
            <li>
                <div class="vue-dropdown" @click="ClicktoggleDropdown(0)" @mouseover="toggleDropdown(0)" @mouseout="toggleDropdown(0)">
                    <div class="filter-btn large-menu-btn d-flex justify-content-between btn align-items-center border-0" type="button">
                        Atualização
                        <IconsSort class="action-icon"/>    
                    </div>
                    <ul class="vue-dropdown-menu" v-show="dropdownStates[0]">
                        <li class="small-menu">
                            <div @click="sendDataToParent('', false)" class="filter-btn d-flex justify-content-between text-align-center align-items-center btn btn-transparent border-0" type="button">
                                asc 
                                <IconsUpArrow class="action-icon"/>
                            </div>
                            <div @click="sendDataToParent('', true)" class="filter-btn d-flex justify-content-between text-align-center align-items-center btn btn-transparent border-0" type="button">
                                dec
                                <IconsBottomArrow class="action-icon"/>
                            </div>
                        </li>
                    </ul>
                </div>
            </li>
            <li>
                <div class="vue-dropdown" @click="ClicktoggleDropdown(1)"  @mouseover="toggleDropdown(1)" @mouseout="toggleDropdown(1)">
                    <div  class="filter-btn large-menu-btn d-flex justify-content-between btn align-items-center border-0" type="button">
                        Criação
                        <IconsClock class="action-icon"/>
                    </div>
                    <ul class="vue-dropdown-menu" v-show="dropdownStates[1]">
                        <li class="small-menu">
                            <div @click="sendDataToParent('id,asc', false)" class="filter-btn d-flex justify-content-between text-align-center align-items-center btn btn-transparent border-0" type="button">
                                asc
                                <IconsUpArrow class="action-icon"/>
                            </div>
                            <div @click="sendDataToParent('id,desc', false)" class="filter-btn d-flex justify-content-between text-align-center align-items-center btn btn-transparent border-0" type="button">
                                dec
                                <IconsBottomArrow class="action-icon"/>
                            </div>
                        </li>
                    </ul>
                </div>
            </li>
            <li>
                <div class="vue-dropdown"  @click="ClicktoggleDropdown(2)"  @mouseover="toggleDropdown(2)" @mouseout="toggleDropdown(2)">
                    <div class="filter-btn large-menu-btn d-flex justify-content-between btn align-items-center border-0" type="button">
                        Nome
                        <IconsNameSort class="action-icon"/>
                    </div>
                    <ul class="vue-dropdown-menu" v-show="dropdownStates[2]">
                        <li class="small-menu">
                            <div @click="sendDataToParent('name,asc', false)" class="filter-btn d-flex justify-content-between text-align-center align-items-center btn btn-transparent border-0" type="button">
                                asc
                                <IconsUpArrow class="action-icon"/>
                            </div>
                            <div @click="sendDataToParent('name,desc', false)" class="filter-btn d-flex justify-content-between text-align-center align-items-center btn btn-transparent border-0" type="button">
                                dec
                                <IconsBottomArrow class="action-icon"/>
                            </div>
                        </li>
                    </ul>
                </div>
            </li>
            <li>
                <div class="vue-dropdown" @click="ClicktoggleDropdown(3)"  @mouseover="toggleDropdown(3)" @mouseout="toggleDropdown(3)">
                    <div class="filter-btn large-menu-btn d-flex justify-content-between btn align-items-center border-0" type="button">
                        Quantidade
                        <IconsQuantitySort class="action-icon"/>
                    </div>
                    <ul class="vue-dropdown-menu" v-show="dropdownStates[3]">
                        <li class="small-menu">
                            <div @click="sendDataToParent('quantity,asc', false)" class="filter-btn d-flex justify-content-between text-align-center align-items-center btn btn-transparent border-0" type="button">
                                asc
                                <IconsUpArrow class="action-icon"/>
                            </div>
                            <div @click="sendDataToParent('quantity,desc', false)" class="filter-btn d-flex justify-content-between text-align-center align-items-center btn btn-transparent border-0" type="button">
                                dec
                                <IconsBottomArrow class="action-icon"/>
                            </div>
                        </li>
                    </ul>
                </div>
            </li>
        </ul>   
    </div>  
</template>

<script setup>
import { inject, onMounted} from 'vue';
import { useUser } from '../../stores/user';
import { useStorageStore } from '../../stores/storage';



const toolTip = ref(false);
const store = useStorageStore();

const dropdownStates = ref([false, false, false, false]);
const toggleDropdown = (dropdown_id) => {
    dropdownStates.value[dropdown_id-1] = false
    dropdownStates.value[dropdown_id] = !dropdownStates.value[dropdown_id]
    dropdownStates.value[dropdown_id+1] = false
}
const ClicktoggleDropdown = (dropdown_id) => {
    if(!store.isMobile){
        return 0
    }
    dropdownStates.value[dropdown_id-1] = false
    dropdownStates.value[dropdown_id] = !dropdownStates.value[dropdown_id]
    dropdownStates.value[dropdown_id+1] = false
}

const setItemsFilter = inject('setItemsFilter')
const sendDataToParent = (filter, isInverted) => {
    setItemsFilter(filter, isInverted)
}

onMounted(() => {
    if(store.isMobile){
        const btnText = document.querySelectorAll('.filter-btn');
        const dropdownToggle = document.querySelector('.dropdown-principal');
        dropdownToggle.removeAttribute('data-bs-auto-close')
        dropdownToggle.setAttribute('data-bs-auto-close', 'outside')
        btnText.forEach(element => element.style.fontSize = '9px');
    }
})
</script>

<style scoped>
li{
    list-style-type: none;
}
.large-menu{
    width: 136px;
    min-width: 40px;
}
.small-menu{
    background-color: white;
    border-radius: 12px;
    border: 1px #D9D9D9 solid;
    position: absolute;
    margin-top: -55px;
    left: 127px;
    width: 65px;
    height: 65px;
    min-width: 40px;
}

.dropdown-item{
    width: 130px;
    padding: 0px;
}
.large-menu-btn{
    font-size: 14px;
}
.btn-transparent{
    font-size: 14px;
}
.action-btn{
    border: none;
    border-radius: 10px 10px 0px 0px;
    border-bottom: 1px ridge #1F69B1;
}
.btn-transparent:hover{
    color: white;
    background-color: #FED51E;
}
.btn-outline-ligth:hover{
    color: white !important; 
    background-color: #0B3B69 !important; 
}
@media screen and (max-width: 820px){
    .action-btn{
        font-size: 12px;
    }
    .filter-btn{
        font-size: 12px;
    }
    .large-menu{
        padding: 0;
        width: 120px !important;
    }
    .small-menu{
        padding: 0;
        margin-top: -40px;
        height: 55px;
        left: 115px;
    }
    .action-icon{
        width: 15px;
        height: 15px;
    }
}
</style>