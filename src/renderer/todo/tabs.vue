<template>
    <div class="helper">
        <span class="left" v-if="unFinishTodoLength == 0">暂时没有急需完成的事项哦</span>
        <span class="left" v-else>
            {{unFinishTodoLength}}件待完成事项
        </span>
        <span class="tabs">
            <span v-for="state in states" :key="state" :class="[state,filter===state? 'active':'']" @click="toggleFilter(state)">
                {{state}}
            </span>
        </span>
        <span class="clear" @click="clearAllCompleted()"></span>
    </div>
</template>
<script>
    export default {
      props: {
        filter: {
          type: String,
          required: true
        },
        todos: {
          type: Array,
          required: true
        }
      },
      data () {
        return {
          states: ['all', 'active', 'completed']
        }
      },
      computed: {
        unFinishTodoLength () {
          return this.todos.filter(todo => !todo.completed).length
        }
      },
      methods: {
        clearAllCompleted () {
          this.$emit('clearAll')
        },
        toggleFilter (state) {
          this.$emit('toggle', state)
        }
      }
    }
</script>
<style lang="less" scoped>
    .helper {
        width: 100%;
        font-weight: 100;
        display: flex;
        justify-content: space-between;
        padding: 5px 0;
        line-height: 30px;
        background-color: #fff;
        font-size: 14px;
        font-smoothing: antialiased;
        display: flex;
        .left, .clear, .tabs {
            padding: 0 10px;
            box-sizing: border-box;
        }
        /*.left, .clear {*/
            /*width: 150px;*/
        /*}*/
        .left {
            flex: 50%;
            text-align: left;
        }
        .clear {
            flex: 10%;
            text-align: right;
            cursor: pointer;
        }
        .tabs {
            flex: 40%;
            /*width: 200px;*/
            display: flex;
            justify-content: space-around;
            * {
                display: inline-block;
                padding: 0 10px;
                cursor: pointer;
                border: 1px solid rgba(175, 47, 47, 0);
                &.actived {
                    border-color: rgba(175, 47, 47, 0.4);
                    border-radius: 5px;
                }
            }
        }
    }


</style>
