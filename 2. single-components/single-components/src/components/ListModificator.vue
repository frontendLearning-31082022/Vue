<template>
    <div>
        <table>
            Список для модификаций
            <tr>
                <th v-for="(i, nameCol) in modelValue[0]" :key='nameCol'>
                    <span class="arrow up" @click="sortColumn(nameCol, $event.target)"></span>
                </th>
            </tr>

            <tr v-for="(item, index) in modelValue" :key='index'>
                <th>{{ item.name }}</th>
                <th>{{ item.price }}</th>
            </tr>
        </table>
    </div>
</template>

<script>

export default {
    name: "ListModificator",
    props: ['modelValue'],
    emits: ['update:modelValue'],
    data() {
        return {
            styleObject: {
                arrow: {
                    color: "red"
                }
            }
        }
    },
    methods: {
        sortColumn(nameCol, arrowDom) {
            let classList = arrowDom.classList;

            let dir = classList.contains('up') ? -1 : 1;

            arrowDom.classList.remove('up');
            arrowDom.classList.remove('down');
            arrowDom.classList.add(dir === 1 ? 'up' : 'down');

            const mutabBag = [... this.modelValue]

            let comparator = function compare(a, b) {
                if (a[nameCol] < b[nameCol]) return -1*dir;
                if (a[nameCol] > b[nameCol]) return 1*dir;
                return 0;
            }
            mutabBag.sort(comparator);

            this.$emit('update:modelValue', mutabBag);
        }
    }
}
</script>

<style lang="scss" scoped>

table {
    border: inset #c89090;
}

.arrow {
    $arrowSize: 10px;
    $arrowBorderSize: 3px;
    $arrowBarWidth: 2px;
    $arrowBarHeight: 15px;

    margin: 5px;
    color: #80c5cc;
    display: inline-block;
    height: 20px;
    position: relative;
    width: 20px;

    @mixin rotate($angle) {
        -moz-transform: rotate($angle);
        -ms-transform: rotate($angle);
        -webkit-transform: rotate($angle);
        transform: rotate($angle);
    }

    &.up {
        @include rotate(225deg);
    }

    &.down {
        @include rotate(45deg);
    }

    &::after {
        border-bottom-style: solid;
        border-bottom-width: $arrowBorderSize;
        border-right-style: solid;
        border-right-width: $arrowBorderSize;
        content: '';
        display: inline-block;
        height: $arrowSize;
        left: 0;
        position: absolute;
        top: 0;
        width: $arrowSize;
    }

    &.is-triangle::after {
        border-style: solid;
        border-width: 0 0 $arrowSize $arrowSize;
        height: 0;
        width: 0;
    }

    &.arrow-bar::before {
        bottom: 1px;
        content: '';
        height: $arrowBarHeight;
        position: absolute;
        right: 0;
        transform-origin: bottom;
        width: $arrowBarWidth;
        @include rotate(-45deg);
    }

}
</style>