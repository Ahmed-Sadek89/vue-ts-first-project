<template>
<div class="job-list">
    <p>ordered by {{order}}</p>
    <ul>
    <li v-for="job in OrderData" :key="job.id">
        <h2>{{ job.title }} in {{ job.location }}</h2>
        <div class="salary">
        <p>{{ job.salary }} rupees</p>
        </div>
        <div class="description">
        <p>Lorem ipsum dolor sit amet consectetur, adipisicing elit. Rem omnis voluptatum eius doloremque optio iusto sequi dignissimos. Pariatur earum assumenda dolores possimus quidem quam, reprehenderit aliquid consequuntur amet non facere.</p>
        </div>
    </li>
    </ul>
</div>
</template>

<script lang="ts">
import Jobs from '@/Types/Jobs';
import OrderTerm from '@/Types/OrderTerm';
import { computed, defineComponent, PropType } from 'vue'

export default defineComponent({
    name: "JobList",
    props: {
        Jobs: {
            required: true,
            type: Array as PropType<Jobs[]>
        },
        order: {
          required: true,
          type: String as PropType<OrderTerm>
        }
    },
    setup(props) {
      const OrderData = computed(() => {
        return [...props.Jobs].sort((a: Jobs, b: Jobs) => {
          return a[props.order] > b[props.order] ? 1 : -1
        })
      })
      return {
        OrderData
      }
    }
})
</script>

<style scoped>
    .job-list {
      max-width: 960px;
      margin: 40px auto;
    }
    .job-list ul {
      padding: 0;
    }
    .job-list li {
      list-style-type: none;
      background: white;
      padding: 16px;
      margin: 16px 0;
      border-radius: 4px;
    }
    .job-list h2 {
      margin: 0 0 10px;
      text-transform: capitalize;
    }
    .salary {
      display: flex;
    }
    .salary img {
      width: 30px;
    }
    .salary p {
      color: #17bf66;
      font-weight: bold;
      margin: 10px 4px;
    }
</style>