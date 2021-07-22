<template>
<div id="transferPanel">
        <ValidationObserver ref="observer" v-slot="{ invalid }">
                <div>
                        <localization :language="'en'">
                                    <intl :locale="'en-GB'">
                                        <ValidationProvider name="Amount" v-slot="{ errors }" rules="required|min_value:0.01" vid="amount">
                                            <numeric-textbox :default-value="0.00" :min="0.01" :format="formatOptions" :spinners="false" v-model="transferAmount" :style="cssWidth" />
                                            <div class="col-12">   <span v-show="errors.length" class="text-danger">{{ errors[0] }}</span>
                                            </div>
                                        </ValidationProvider>
                                    </intl>
                              </localization>
                  </div>
        </ValidationObserver>
</div>
</template>

<script>
    
    import { DropDownList } from "@progress/kendo-dropdowns-vue-wrapper";
    import { DatePicker } from "@progress/kendo-dateinputs-vue-wrapper";
    import { NumericTextBox } from '@progress/kendo-vue-inputs';
    import moment from 'moment';
    import { Window } from '@progress/kendo-window-vue-wrapper';
    import { Dialog, DialogActionsBar } from '@progress/kendo-vue-dialogs';
    import { IntlProvider, load, LocalizationProvider, loadMessages } from '@progress/kendo-vue-intl';

    import likelySubtags from 'cldr-core/supplemental/likelySubtags.json';
    import currencyData from 'cldr-core/supplemental/currencyData.json';
    import numbers from 'cldr-numbers-full/main/en-GB/numbers.json';
    import currencies from 'cldr-numbers-full/main/en-GB/currencies.json';

    load(likelySubtags, currencyData, numbers, currencies);
    import { ValidationObserver, ValidationProvider, extend, } from 'vee-validate';
    import { digits, required, min_value } from 'vee-validate/dist/rules';
    extend('required', required);
    extend('digits', digits);
    extend('min_value', min_value);


    export default {
        name: "BankDialog",
        props: {
            
        },
        data: () => ({
            transferAmount: 0.0,
            transactionDate: moment().startOf('day').format(),
            formatOptions: {
                style: 'currency',
                currency: 'GBP',
                currencyDisplay: 'symbol'
            },
        }),


        mixins: [],
        inject: [],
        watch: {
                    },
        created: function () {
        },
        mounted: function () {
        },
        computed: {
            cssWidth: function () {
                return {
                    width: '290px'
                }
            },
        },
        methods: {
            resetData: function () {
            },
        
        },
        components: {
            "dropdown": DropDownList,
            "datepicker": DatePicker,
            "numeric-textbox": NumericTextBox,
            window: Window,
            intl: IntlProvider,
            localization: LocalizationProvider,
            ValidationProvider,
            ValidationObserver
        }
    }

</script>