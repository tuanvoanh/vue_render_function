<script>
import {h} from 'vue'
export default {
    props: {
        level: {
            default: 1
        }
    },
    setup({level}, {slots}) {
        const slot = slots.default ? slots.default() : []
        console.log('slot:', slot)
        const modifiedSLot = slot.map( ( {children} ) => {
            return h("div", { style: "color: purple"}, children)
        })
        return () => h(`h${level}`, {class: "heading"}, modifiedSLot)
    }
}
</script>
<style>
.heading {
    padding-bottom: 10px;
}
</style>