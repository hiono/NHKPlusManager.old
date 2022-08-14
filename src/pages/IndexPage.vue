  <template>
    <q-page class="flex flex-center">
      <div>
        <q-btn outline rounded color="primary" label="increment" @click="incr">: {{counter}}*2={{doubleCount}}</q-btn>
        <q-btn outline rounded color="primary" label="decrement" @click="test.decrement()">: {{counter}}*2={{doubleCount}}</q-btn>
        <q-btn outline rounded color="primary" label="Reset" @click="test.$reset()"></q-btn>
        <q-btn outline rounded color="primary" label="Patch" @click="patch"></q-btn>
      </div>
    </q-page>
    </template>

    <script>
  import { defineComponent } from 'vue'

import {useTestStore} from '../stores/test'
import {storeToRefs} from 'pinia'

export default defineComponent({
  name: 'IndexPage',
  setup()
  {
    // ストアの呼び出し
    const test = useTestStore()

    // ストアプロパティの取得
    // toRefsだとreactivityが壊れるので注意
    const {counter, doubleCount} = storeToRefs(test)

    // ストアアクションの取得
    const incr = () => {
      test.increment()
    };

    // 特定値に強制初期化
    const patch = () => {
      test.$patch({
        counter: 100
      });
    };

    return {
      test,
      counter,
      doubleCount,
      incr,
    };
  },
})
  </script>
