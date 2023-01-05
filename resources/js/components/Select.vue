<template>
    <div class='flex flex-col md:flex-row'>
        <div class="px-6 md:px-8 mt-2 md:mt-0 pb-5 w-full md:w-4/5 md:py-5">
            <span>Select content language:</span>
            <div class="relative w-full mt-2">
                <v-select
                    :options="mappedOptions"
                    :class="['form-control form-select form-select-bordered', classNames]"
                    :modelValue="value"
                    :reduce="option => option.code"
                    @update:modelValue="input"
                    :clearable="false"
                ></v-select>
            </div>
        </div>
    </div>
</template>

<script>

import 'vue-select/dist/vue-select.css';

export default {
    props: ['options', 'classNames', 'value', 'input', 'requiredLanguages'],
    data() {
        return {
            mappedOptions: Object.entries(this.options)?.map(([key, value]) => {
                const label = (this.requiredLanguages && this.requiredLanguages[value] !== undefined && this.requiredLanguages[value] == true) ? key + ' *' : key;
                return ({label: label, code: value})
            } ) || []
        }
    }

}

</script>

<style scoped>
:global(.dark){
    --vs-custom-color: #664cc3;
    --vs-custom-background: #282c34;

    --vs-controls-color: rgba(var(--colors-gray-400));

    --vs-dropdown-bg: rgba(var(--colors-gray-900));
    --vs-dropdown-color: rgba(var(--colors-gray-400));
    --vs-dropdown-option-color: rgba(var(--colors-gray-400));

    --vs-selected-bg: rgba(var(--colors-gray-400));
    --vs-selected-color: #eeeeee;

    --vs-search-input-color: #eeeeee;

    --vs-dropdown-option--active-bg: rgba(var(--colors-gray-400));
    --vs-dropdown-option--active-color: #eeeeee;
}

:deep(.vs__dropdown-toggle) {
    border-width: 0;
}
</style>
