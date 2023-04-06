<template>
  <div class="bg-white shadow sm:rounded-lg">
    <div class="px-4 py-5 sm:p-6">
      <h3 class="text-base font-semibold leading-6 text-gray-900">Calculate ISBN</h3>
      <div class="mt-2 max-w-xl text-sm text-gray-500">
        <p>Enter your value e.g 978014300723 to calculate ISBN e.g 9780143007234</p>
      </div>
      <form class="mt-5 sm:flex sm:items-center">
        <div class="w-full sm:max-w-xs">
          <label for="email" class="sr-only">Email</label>
          <input
            v-model="isbn"
            type="text"
            name="ISBN"
            id="isbn"
            class="block w-full rounded-md border-0 py-1.5 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:text-sm sm:leading-6"
            placeholder="978014300723"
          />
        </div>
        <button
          @click="calculate"
          type="button"
          class="mt-3 inline-flex w-full items-center justify-center rounded-md bg-indigo-600 px-3 py-2 text-sm font-semibold text-white shadow-sm hover:bg-indigo-500 focus-visible:outline focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-indigo-600 sm:ml-3 sm:mt-0 sm:w-auto"
        >
          Calculate
        </button>
      </form>
    </div>

    <div class="flex" v-if="result.length > 1">
      <div class="flex-shrink-0">
        <CheckCircleIcon class="h-5 w-5 text-green-400" aria-hidden="true" />
      </div>
      <div class="ml-3">
        <p class="text-sm font-medium text-green-800">Completed ISBN: {{ result }}</p>
      </div>
      <div class="ml-auto pl-3">
        <div class="-mx-1.5 -my-1.5"></div>
      </div>
    </div>
  </div>
</template>
<script lang="ts">
import { CheckCircleIcon } from '@heroicons/vue/20/solid'
export default {
  data() {
    return {
      result: '',
      isbn: ''
    }
  },
  components: {
    CheckCircleIcon
  },
  methods: {
    calculate() {
      const isbn = this.isbn
      let sum = 0
      for (let i = 0; i < isbn.length; i++) {
        if (i % 2 === 0) {
          sum += parseInt(isbn.charAt(i)) * 1
        } else {
          sum += parseInt(isbn.charAt(i)) * 3
        }
      }
      let mod = sum % 10
      let checkDigit = (10 - mod) % 10
      this.result = isbn + checkDigit
    }
  }
}
</script>
