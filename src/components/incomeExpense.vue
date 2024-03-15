<script lang="ts" setup>
    import { defineProps } from 'vue';

    const props = defineProps({
        income: {
            type: Number,
            required: true
        },
        expenses: {
            type: Number,
            required: true
        }
    });
</script>

<template>
    <div class="inc-exp-container">
        <div>
            <h4>Income</h4>
            <p id="moneyPlus" class="money plus">+${{ props.income }}</p>
        </div>
        <div>
            <h4>Expense</h4>
            <p id="moneyMinus" class="money minus">-${{ props.expenses }}</p>
        </div>
    </div>
</template>
