
<template>
  <div class="overflow-hidden bg-white shadow sm:rounded-lg">
    <div class="px-4 py-5 sm:px-6">
      <h3 class="text-lg font-medium leading-6 text-gray-900">
        {{ item.dict.room }}
      </h3>
      <p class="max-w-2xl mt-1 text-sm text-gray-500">
        Details and application.
      </p>
    </div>
    <div
    class="border-t border-gray-200"
    v-for="element in item.dict.data_types.elements"
    v-bind:key="element"
    >
      <dl>
        <div class="px-4 py-5 bg-gray-50 sm:grid sm:grid-cols-3 sm:gap-4 sm:px-6">
          <dt class="text-sm font-medium text-gray-500">
            Name
          </dt>
          <dd
          class="mt-1 text-sm text-gray-900 sm:mt-0 sm:col-span-2"
          >
            <ul
            role="list" class="border border-gray-200 divide-y divide-gray-200 rounded-md">
              <li
              class="flex items-center justify-between py-3 pl-3 pr-4 text-sm"
              v-for="(value, key) in element.details.elements"
              v-bind:key="key"
              >
                <div class="flex items-center flex-1 w-0">
                  <span class="flex-1 w-0 ml-2 truncate">
                    {{ key }}
                  </span>
                </div>
                <div class="flex-shrink-0 ml-4">
                  <a href="#" class="font-medium text-indigo-600 hover:text-indigo-500">
                    Review
                  </a>
                </div>
              </li>
            </ul>
          </dd>
        </div>
        <div class="px-4 py-5 bg-white sm:grid sm:grid-cols-3 sm:gap-4 sm:px-6">
          <dt class="text-sm font-medium text-gray-500">
            Data Subjects
          </dt>
          <dd class="mt-1 text-sm text-gray-900 sm:mt-0 sm:col-span-2">
            <!-- {{ element.indiv }} -->
          </dd>
        </div>
        <div class="px-4 py-5 bg-gray-50 sm:grid sm:grid-cols-3 sm:gap-4 sm:px-6">
          <dt class="text-sm font-medium text-gray-500">
            Exporting Country
          </dt>
          <dd class="mt-1 text-sm text-gray-900 sm:mt-0 sm:col-span-2">
            <!-- {{ element.exporting_country.name }} -->
          </dd>
        </div>
        <div class="px-4 py-5 bg-white sm:grid sm:grid-cols-3 sm:gap-4 sm:px-6">
          <dt class="text-sm font-medium text-gray-500">
            Importing Country
          </dt>
          <dd class="mt-1 text-sm text-gray-900 sm:mt-0 sm:col-span-2">
            <!-- {{ element.importing_country.name }} -->
          </dd>
        </div>
        <div class="px-4 py-5 bg-gray-50 sm:grid sm:grid-cols-3 sm:gap-4 sm:px-6">
          <dt class="text-sm font-medium text-gray-500">
            Purpose
          </dt>
          <dd class="mt-1 text-sm text-gray-900 sm:mt-0 sm:col-span-2">
            <!-- {{ element.purpose }} -->
          </dd>
        </div>
        <div class="px-4 py-5 bg-white sm:grid sm:grid-cols-3 sm:gap-4 sm:px-6">
          <dt class="text-sm font-medium text-gray-500">
            Attachments
          </dt>
          <dd class="mt-1 text-sm text-gray-900 sm:mt-0 sm:col-span-2">
            <ul role="list" class="border border-gray-200 divide-y divide-gray-200 rounded-md">
              <li class="flex items-center justify-between py-3 pl-3 pr-4 text-sm">
                <div class="flex items-center flex-1 w-0">
                  <!-- Heroicon name: solid/paper-clip -->
                  <svg class="flex-shrink-0 w-5 h-5 text-gray-400" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 20 20" fill="currentColor" aria-hidden="true">
                    <path fill-rule="evenodd" d="M8 4a3 3 0 00-3 3v4a5 5 0 0010 0V7a1 1 0 112 0v4a7 7 0 11-14 0V7a5 5 0 0110 0v4a3 3 0 11-6 0V7a1 1 0 012 0v4a1 1 0 102 0V7a3 3 0 00-3-3z" clip-rule="evenodd" />
                  </svg>
                  <span class="flex-1 w-0 ml-2 truncate">
                    resume_back_end_developer.pdf
                  </span>
                </div>
                <div class="flex-shrink-0 ml-4">
                  <a href="#" class="font-medium text-indigo-600 hover:text-indigo-500">
                    Download
                  </a>
                </div>
              </li>
              <li class="flex items-center justify-between py-3 pl-3 pr-4 text-sm">
                <div class="flex items-center flex-1 w-0">
                  <!-- Heroicon name: solid/paper-clip -->
                  <svg class="flex-shrink-0 w-5 h-5 text-gray-400" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 20 20" fill="currentColor" aria-hidden="true">
                    <path fill-rule="evenodd" d="M8 4a3 3 0 00-3 3v4a5 5 0 0010 0V7a1 1 0 112 0v4a7 7 0 11-14 0V7a5 5 0 0110 0v4a3 3 0 11-6 0V7a1 1 0 012 0v4a1 1 0 102 0V7a3 3 0 00-3-3z" clip-rule="evenodd" />
                  </svg>
                  <span class="flex-1 w-0 ml-2 truncate">
                    coverletter_back_end_developer.pdf
                  </span>
                </div>
                <div class="flex-shrink-0 ml-4">
                  <a href="#" class="font-medium text-indigo-600 hover:text-indigo-500">
                    Download
                  </a>
                </div>
              </li>
            </ul>
          </dd>
        </div>
      </dl>
    </div>
  </div>
</template>

<script>

export default {
  props: {
    item: {
      type: Object,
      required: true,
    },
  },
}
</script>
