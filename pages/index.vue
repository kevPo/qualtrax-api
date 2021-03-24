<template>
  <div
    v-if="!deleting"
    class="flex items-center min-h-screen bg-gray-50 dark:bg-gray-900"
  >
    <div class="container mx-auto">
      <div class="max-w-md mx-auto my-10 bg-white p-5 rounded-md shadow-sm">
        <div class="text-center">
          <h1
            class="my-3 text-3xl font-semibold text-gray-700 dark:text-gray-200"
          >
            Qualtrax Delete WF Instances
          </h1>
        </div>
        <div class="m-7">
          <div class="mb-6">
            <label
              for="url"
              class="block mb-2 text-sm text-gray-600 dark:text-gray-400"
              >URL</label
            >
            <input
              type="text"
              v-model="url"
              name="url"
              id="url"
              placeholder="https://our.qualtraxcloud.com"
              required
              class="w-full px-3 py-2 placeholder-gray-300 border border-gray-300 rounded-md focus:outline-none focus:ring focus:ring-indigo-100 focus:border-indigo-300 dark:bg-gray-700 dark:text-white dark:placeholder-gray-500 dark:border-gray-600 dark:focus:ring-gray-900 dark:focus:border-gray-500"
            />
          </div>
          <div class="mb-6">
            <label
              for="token"
              class="block mb-2 text-sm text-gray-600 dark:text-gray-400"
              >API Token</label
            >
            <input
              type="text"
              v-model="token"
              name="token"
              id="token"
              required
              class="w-full px-3 py-2 placeholder-gray-300 border border-gray-300 rounded-md focus:outline-none focus:ring focus:ring-indigo-100 focus:border-indigo-300 dark:bg-gray-700 dark:text-white dark:placeholder-gray-500 dark:border-gray-600 dark:focus:ring-gray-900 dark:focus:border-gray-500"
            />
          </div>
          <div class="mb-6">
            <label
              for="name"
              class="block mb-2 text-sm text-gray-600 dark:text-gray-400"
              >Application Name</label
            >
            <input
              type="text"
              v-model="name"
              name="name"
              id="name"
              placeholder="qualtrax"
              required
              class="w-full px-3 py-2 placeholder-gray-300 border border-gray-300 rounded-md focus:outline-none focus:ring focus:ring-indigo-100 focus:border-indigo-300 dark:bg-gray-700 dark:text-white dark:placeholder-gray-500 dark:border-gray-600 dark:focus:ring-gray-900 dark:focus:border-gray-500"
            />
          </div>
          <div class="mb-6">
            <label
              for="reason"
              class="block mb-2 text-sm text-gray-600 dark:text-gray-400"
              >Deletion Reason</label
            >
            <input
              type="text"
              v-model="reason"
              name="reason"
              id="reason"
              placeholder="Blank Workflows"
              required
              class="w-full px-3 py-2 placeholder-gray-300 border border-gray-300 rounded-md focus:outline-none focus:ring focus:ring-indigo-100 focus:border-indigo-300 dark:bg-gray-700 dark:text-white dark:placeholder-gray-500 dark:border-gray-600 dark:focus:ring-gray-900 dark:focus:border-gray-500"
            />
          </div>
          <div class="mb-6">
            <label
              for="ids"
              class="block mb-2 text-sm text-gray-600 dark:text-gray-400"
              >Ids to Delete:</label
            >
            <textarea
              rows="5"
              v-model="ids"
              name="ids"
              id="ids"
              placeholder="234, 232, 123, 456"
              class="w-full px-3 py-2 placeholder-gray-300 border border-gray-300 rounded-md focus:outline-none focus:ring focus:ring-indigo-100 focus:border-indigo-300 dark:bg-gray-700 dark:text-white dark:placeholder-gray-500 dark:border-gray-600 dark:focus:ring-gray-900 dark:focus:border-gray-500"
              required
            ></textarea>
          </div>
          <div class="mb-6">
            <button
              @click="deleteInstances"
              class="w-full px-3 py-4 text-white bg-indigo-500 rounded-md focus:bg-indigo-600 focus:outline-none"
            >
              Delete
            </button>
          </div>
          <p class="text-base text-center text-gray-400" id="result"></p>
        </div>
      </div>
    </div>
  </div>
  <div v-else>
    <h1>hi there!</h1>
    <p>{{ url }}</p>
    <p>{{ token }}</p>
    <p>{{ name }}</p>
    <p>{{ reason }}</p>
  </div>
</template>

<script>
export default {
  data() {
    return {
      url: "",
      token: "",
      name: "",
      reason: "",
      ids: "",
      deleting: false,
    };
  },
  methods: {
    deleteInstances() {
      var bodyObject = { deletionReason: this.reason };
      var body = JSON.stringify(bodyObject);
      var headers = {
        "Content-Type": "application/json",
        "Accept": "application/vnd.qualtrax.v1+json",
        "Authorization": `Bearer ${this.token}`,
        "User-Agent": `${this.name}`
      };

      var instanceIds = this.ids.split(", ");
      var fetches = [];
      debugger;
      fetch(`${this.url}/api/workflows/${instanceIds[0]}`, {
            method: "DELETE",
            headers: {
              "Content-Type": "application/json",
              "Accept": "application/vnd.qualtrax.v1+json",
              "Authorization": `Bearer ${this.token}`,
              "User-Agent": `${this.name}`
            },
            body: body,
          })
          .then((response) => {
            debugger;
            // let json = await response.json();
            // console.log(json);
            console.log(response);
          })
          .catch((error) => {
            debugger;
            console.log(error);
          })

      // for (let i = 0; i < instanceIds.length; i++) {
      //   fetches.push(
          
      //   );
      // }

      // Promise.all(fetches).then(function() {
      //   console.log('DONE');
      // });

      this.deleting = true;
    },
  },
};
</script>

<style>
</style>
