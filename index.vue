<template lang="html">
    <div class="dynamic-form-fields">
        <form v-if="fullForm" method="post" @submit.prevent="processData(fieldsOrderedBy)">
            <div class="form-section" v-for="field in fieldsOrderedBy">
                <div :class="field.wrapperClass">

                    <label v-if="field.showLabel">{{ field.label }}</label>

                    <select v-if="field.type === 'select'" :name="field.name" :class="field.cssClass" v-model="field.value">
                        <option v-if="field.options.length" v-for="option in field.options" :value="option" >{{ option }}</option>
                    </select>

                    <div v-if="field.type === 'checkbox'" :class="field.cssClass">
                        <span v-for="option in field.options">
                            <label>
                                <input type="checkbox" :name="field.name" :value="option" v-model="field.value">
                                <span>{{ option }}</span>
                            </label>
                        </span>
                    </div>

                    <div v-if="field.type === 'radio'" :class="field.cssClass">
                        <span v-for="option in field.options">
                            <label>
                                <input type="radio" :name="field.name" :value="option" v-model="field.value">
                                <span>{{ option }}</span>
                            </label>
                        </span>
                    </div>

                    <input v-if="field.type === 'text' || field.type === 'email' || field.type === 'password' || field.type === 'hidden'"
                        :type="field.type"
                        :name="field.name"
                        :placeholder="field.placeholder"
                        :class="field.cssClass"
                        :value="field.value"
                        @input="field.value = $event.target.value"
                    >

                    <textarea v-if="field.type === 'textarea'"
                    :name="field.name"
                    :placeholder="field.placeholder"
                    :class="field.cssClass"
                    v-model="field.value"
                    ></textarea>

                    <span v-if="field.type === 'html'" v-html="field.html" :class="field.cssClass"></span>

                    <button v-if="field.type === 'button'" :class="field.cssClass" type="submit" :name="field.name" >{{ field.buttonText }}</button>
                </div>
            </div>
        </form>

        <div v-if="!fullForm">
            <div class="form-section" v-for="field in fieldsOrderedBy">
                <div :class="field.wrapperClass">

                    <label v-if="showLabel">{{ field.label }}</label>

                    <select v-if="field.type === 'select'" :name="field.name" :class="field.cssClass" v-model="field.value">
                        <option v-if="field.options.length" v-for="option in field.options" :value="option" >{{ option }}</option>
                    </select>

                    <div v-if="field.type === 'checkbox'" :class="field.cssClass">
                        <span v-for="option in field.options">
                            <label>
                                <input type="checkbox" :name="field.name" :value="option" v-model="field.value">
                                <span>{{ option }}</span>
                            </label>
                        </span>
                    </div>

                    <div v-if="field.type === 'radio'" :class="field.cssClass">
                        <span v-for="option in field.options">
                            <label>
                                <input type="radio" :name="field.name" :value="option" v-model="field.value">
                                <span>{{ option }}</span>
                            </label>
                        </span>
                    </div>

                    <div :class="field.wrapperClass">
                        <input v-if="field.type === 'text' || field.type === 'email' || field.type === 'password'"
                            :type="field.type"
                            :name="field.name"
                            :placeholder="field.placeholder"
                            :class="field.cssClass"
                            :value="field.value"
                            @input="field.value = $event.target.value"
                        >
                    </div>

                    <div :class="field.wrapperClass">
                        <textarea v-if="field.type === 'textarea'"
                        :name="field.name"
                        :placeholder="field.placeholder"
                        :class="field.cssClass"
                        v-model="field.value"
                        ></textarea>
                    </div>
                </div>

                <span v-if="field.type === 'html'" v-html="field.html" :class="field.cssClass"></span>

                <button v-if="field.type === 'button'" :class="field.cssClass" type="submit" :name="field.name" >{{ field.buttonText }}</button>

            </div>
        </div>
    </div>
</template>

<script>
    /**
     * Imported Dependecies
     */
    import orderBy from 'lodash/orderBy';

    export default {
        name: 'dynamic-fields',

        props: ['fields', 'orderOption', 'fullForm'],

        data() {
            return {
                formData: [],
            };
        },

        methods: {
            /**
             * verify if order criteria is defined
             */
            orderExists(prop) {
                return this.fields.filter(field => field.prop);
            },

            /**
             * Read the curent field Value
             */
            readValue(val, currentField) {
                this.fields.forEach((field) => {
                    if (field.name === currentField.name) {
                        field.value = val;
                    }
                });
            },

            /**
             * process and emit data
             */
            processData(fields) {
                fields.forEach((field) => {
                    this.formData.push({ name: field.name, value: field.value });
                });
                this.$emit('posted', this.formData);
            },
        },

        computed: {
            /**
             * computed property for display list by 'order' if order is defined
             */
            fieldsOrderedBy() {
                if (this.orderExists(this.orderOption)) {
                    return orderBy(this.fields, this.orderOption);
                }
                // else return array as it is
                return this.fields;
            },
        },
    };
</script>
