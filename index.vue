<template lang="html">
    <div class="dynamic-form-fields">

        <div class="form-section" v-for="field in fieldsOrderedBy">

            <label>{{ field.label }}</label>

            <select v-if="field.type === 'select'" :name="field.name" :class="field.cssClass" v-model="field.name">
                <option v-if="field.options.length" v-for="option in field.options" :value="option">{{ option }}</option>
            </select>

            <div v-if="field.type === 'radio'" :class="field.cssClass">
                <span v-for="option in field.options">
                    <label>
                        <input type="radio" :name="field.name" :value="option" v-model="option">
                        <span>{{ option }}</span>
                    </label>
                </span>
            </div>

            <input v-if="field.type === 'text' || field.type === 'email' || field.type === 'password'" :type="field.type" v-model="field.name" :name="field.name" :placeholder="field.placeholder" :class="field.cssClass">

            <span v-if="field.type === 'html'" v-html="field.html" :class="field.cssClass"></span>

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

        /**
         * DOCUMENTATION FOR THIS COMPONENT
         »
         * properties of each object
         *
         * fields:
            type: str - select, text, email, textarea, radio or checkbox
            name: str - input name
            label: str - input label
            placeholder: str - input placeholder text
            order: num - listing order
            options: array - options if the input type is defined as 'Select', 'radio', or 'checkbox'
            is_required: boolean
            cssClass: str - define class names separated by space
                example { cssClass: 'some-input othe-class input-error', }
            html: if a block of html is needed between inputs like warnings, separators, etc.
                example { html: '<p>all fields are required</p>', }
         *
         * orderOption:
            On each instance of this component, it can be defined the order of listing by field
            example:
            <dynamic-fields :fields="configFormDetails" :orderOption="'order'"></dynamic-fields>
         */
        props: ['fields', 'orderOption'],

        methods: {
            /**
             * verify if order criteria is defined
             */
            orderExists(prop) {
                return this.fields.filter(field => field.prop);
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
