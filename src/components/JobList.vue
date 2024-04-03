<template>
    <div class="job-list">
        <p>Ordered by {{ orderTerm }}</p>
        <TransitionGroup name="list" tag="ul">
            <li v-for="job in orderJobs" :key="job.id">
                <h2>{{ job.title }} in {{ job.location }}</h2>
                <div class="salary">
                    <p>{{ job.salary }} rupees</p>
                </div>
                <div class="description">
                    <p>Lorem ipsum dolor sit amet consectetur, adipisicing elit. Rem omnis voluptatum eius doloremque
                        optio iusto sequi dignissimos. Pariatur earum assumenda dolores possimus quidem quam,
                        reprehenderit aliquid consequuntur amet non facere.</p>
                </div>
            </li>
        </TransitionGroup>
    </div>
</template>

<script setup lang="ts">
import { computed, defineProps } from 'vue'
import Job from '@/types/Job'
import OrderTerm from '@/types/OrderTerm'

const props = defineProps<{
    jobs: Job[],
    orderTerm: OrderTerm
}>()


const orderJobs = computed<Job[]>(()=>{
    return [...props.jobs].sort((a: Job, b:Job)=>{
        return a[props.orderTerm] > b[props.orderTerm] ? 1 : -1
    })
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
.list-move, /* 对移动中的元素应用的过渡 */
.list-enter-active,
.list-leave-active {
  transition: all 0.5s ease;
}

.list-enter-from,
.list-leave-to {
  opacity: 0;
  transform: translateX(30px);
}
</style>