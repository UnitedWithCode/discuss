<script setup>
const title = ref('')
const sending = ref(false)
const postIssue = async () => {
  if (sending.value || !title.value.trim()) return
  sending.value = true
  // Call GitHub
  await githubFetch('/repos/atinux/discuss/issues', {
    method: 'POST',
    body: { title: title.value, },
  })
  sending.value = false
  title.value = ''
}
</script>

<template>
  <div>
    <h2 class="text-2xl">New Message</h2>
    <form @submit.prevent="postIssue" class="mt-2 flex">
      <input
        type="text"
        required
        v-model="title"
        placeholder="Your message :)"
        class="flex-1 border px-2 py-1 rounded-l border-r-0"
      />
      <button type="submit" class="border px-2 py-1 rounded rounded-l-0">
        {{ sending ? 'Sending...' : 'Send' }}
      </button>
    </form>
  </div>
</template>
