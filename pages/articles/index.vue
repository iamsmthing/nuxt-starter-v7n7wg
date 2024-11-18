<script setup>
import { useRouter } from 'vue-router';

const router = useRouter();

onMounted(() => {
  router.push('/articles/1');
});
</script>
