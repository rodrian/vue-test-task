<template>
    <div class="todo">
        <h1 class="title">Checklist</h1>
        <ui-tabs type="text">
            <ui-tab title="Pending">
                <ul class="tasks">
                    <li v-for="task in tasks" v-if="!task.complete">
                        <label>
                            <ui-checkbox type="checkbox" v-model="task.complete"
                                class="ui_checkbox" @focus="changeStyle" />
                                <span class="task_name"
                                    :class="{complete : task.complete}">
                                    {{task.name}}
                                </span>
                        </label>
                    </li>
                </ul>
            </ui-tab>
            <ui-tab title="Completed" id="completed">
                <ul class="tasks">
                    <li v-for="task in tasks" v-if="task.complete">
                        <label>
                            <ui-checkbox type="checkbox" v-model="task.complete"
                                class="ui_checkbox" />
                                <span class="task_name"
                                    :class="{complete : task.complete}">
                                    {{task.name}}
                                </span>
                        </label>
                    </li>
                </ul>
            </ui-tab>
        </ui-tabs>
        
        <div>
            <ui-textbox placeholder="e.g. 'read vue.js guide'"
                id="ui_textbox" v-model="newTaskName"></ui-textbox>
            <ui-button color="primary" @click="addTask" icon="add"
                class="ui_button">
                Add
            </ui-button>
        </div>
    </div>
</template>

<script>
    export default {
        data () {
            return {
                newTaskName : '',
                tasks : [
                    {name : 'create skeleton of todo', complete : true},
                    {name : 'add ability to add tasks', complete : true},
                    {name : 'clear task name after clicking "Add"', complete : true},
                    {name : 'put "Add" button in one line with input', complete : true},
                    {name : 'replace <input> with <ui-checkbox> in tasks list', complete : true},
                    {name : 'when task is complete cross it out', complete : true},
                    {name : 'split tasks into "pending" and "complete" tabs using keen-ui component <ui-tabs>', complete : true},
                    {name : 'don\'t allow to add empty tasks', complete : true},
                    {name : 'make list of tasks scrollable, if there\'re are a lot of tasks', complete : true},
                    {name : 'extract list item into a separate vue.js component', complete : false},
                    {name : 'persist tasks list in a local storage', complete : false},
                    {name : 'add animation on task completion', complete : false},
                ]
            }
        },

        methods : {
            addTask () {
                if (this.newTaskName != '') {
                    this.tasks.push({name : this.newTaskName, complete : false});
                }
                this.newTaskName = '';
            },
            changeStyle() {
                var text = document.getElementsByClassName('ui-tab-header-item__text')[1];
                setTimeout(increase, 100);
                function increase() {
                    text.style.fontSize = '16px';
                }
                setTimeout(decrease, 250);
                function decrease() {
                    text.style.fontSize = '14px';
                }
            }
        }
    };
</script>

<style scoped lang="scss">
    .todo {
        margin: auto;
        background: #fff;
        padding: 20px;
        border-radius: 5px;
        box-shadow: rgba(0, 0, 0, 0.3) 3px 3px 15px;

        .title {
            margin-top: 0;
        }

        .tasks {
            list-style: none;
            padding: 0;
            max-height: 356px;
            overflow-y: auto;
        }
        .ui_checkbox {
            display: inline-flex;
        }
        .task_name {
            vertical-align: top;
            margin: 5px;
        }
        .complete {
            text-decoration: line-through;
        }
        #ui_textbox {
            display: inline-flex;
            width: 70%;
        }
        .ui_button {
            margin-left: 10px;
            float: right;
        }
    }
</style>
