<template>
    <el-input :model-value="JSON.stringify(values)" :disabled="true">
        <template #append>
            <el-button
                :icon="TextSearch"
                @click="
                    $store.commit('code/addBreadcrumbs', {
                        breadcrumb: {
                            label: root,
                            to: {},
                            component: h('task-object', {
                                modelValue: modelValue,
                                'onUpdate:modelValue': onInput,
                                schema: currentSchema,
                                definitions: definitions,
                            }),
                        },
                        position:
                            breadcrumbs.length === 2 ? 2 : breadcrumbs.length,
                    })
                "
            />
        </template>
    </el-input>
</template>

<script setup>
    import TextSearch from "vue-material-design-icons/TextSearch.vue";
    import {h} from "vue";
</script>

<script>
    import Task from "./Task";
    import {mapState} from "vuex";

    export default {
        mixins: [Task],
        computed: {
            ...mapState("code", ["breadcrumbs"]),

            currentSchema() {
                let ref = this.schema.$ref.substring(8);
                if (this.definitions[ref]) {
                    return this.definitions[ref];
                }
                return undefined;
            },
        },
    };
</script>
