<template>
  <div class="ctr">
    <!-- 确保questions在result之前完成动画 -->
    <tansition name="fade" mode="out-in">
      <questions
        v-if="questionsAnswered < questions.length"
        :questions="questions"
        :questionsAnswered="questionsAnswered"
        @question-answered="questionAnswered"
      />
      <result v-else :results="results" :totalCorrect="totalCorrect" />
    </tansition>
    <button
      type="button"
      class="reset-btn"
      @click.prevent="reset"
      v-if="questionsAnswered === questions.length"
    >
      再答一次
    </button>
  </div>
</template>

<script>
import Questions from "./components/Questions.vue";
import Result from "./components/Result.vue";
export default {
  name: "App",
  components: {
    Questions,
    Result,
  },
  data() {
    return {
      // 当前问题的特殊索引
      questionsAnswered: 0,
      // 用户正确回答的数量
      totalCorrect: 0,
      questions: [
        {
          q: `秋天（ ）夜晚，明亮（ ）月光照在床前，远离家乡（ ）人望着那天上（ ）月亮，不由（ ）思念起故乡来。`,
          answers: [
            {
              text: `的 的 的 的 得`,
              is_correct: true,
            },
            {
              text: `的 得 的 的 得`,
              is_correct: false,
            },
            {
              text: `的 的 的 的 地`,
              is_correct: false,
            },
          ],
        },
        {
          q: `一次又一次（ ）将满地（ ）鲜花抛向天空。`,
          answers: [
            {
              text: `得 的`,
              is_correct: false,
            },
            {
              text: `地 的`,
              is_correct: true,
            },
            {
              text: `的 的`,
              is_correct: false,
            },
          ],
        },
        {
          q: `天黑了，路灯发出微弱（ ）光芒。我站在伯父家门口看着他们，突然感到凉凉（ ）寒意，摸摸自己（ ）鼻尖，冷（ ）像冰，脚和手也有些麻木了。`,
          answers: [
            {
              text: `的 的 的 得`,
              is_correct: true,
            },
            {
              text: `的 得 的 得`,
              is_correct: false,
            },
            {
              text: `的 的 的 的`,
              is_correct: false,
            },
          ],
        },
        {
          q: `这时候，我清清楚楚（ ）看见，而且现在也清清楚楚（ ）记得，他（ ）脸不再有那种慈祥（ ）愉快（ ）表情了，变（ ）那么严肃。`,
          answers: [
            {
              text: `地 地 的 的 地`,
              is_correct: false,
            },
            {
              text: `地 地 的 的 得`,
              is_correct: true,
            },
            {
              text: `的 的 的 的 得`,
              is_correct: false,
            },
          ],
        },
        {
          q: `焦裕禄出了许楼村，又急急忙忙（ ）向前奔去。他那顶棉帽子（ ）耳巴忽闪忽闪（ ），渐渐（ ）消失在茫茫雪海中。`,
          answers: [
            {
              text: `的 的 得 的`,
              is_correct: false,
            },
            {
              text: `地 的 的 的`,
              is_correct: false,
            },
            {
              text: `地 的 的 地`,
              is_correct: true,
            },
          ],
        },
      ],
      results: [
        {
          min: 0,
          max: 2,
          title: "再试一次!",
          desc: `修饰、限制的词语+的+名词 修饰、限制的词语+地+动词 动词或形容词+得+补充、说明的词语
          学会了吗？再答一次看看吧！下次一定能成功！
          `,
        },
        {
          min: 3,
          max: 4,
          title: "真厉害!",
          desc: "再答一次看看！下次一定能满分！",
        },
        {
          min: 5,
          max: 5,
          title: "Wow, 你是“的、地、得”天才啊!",
          desc: `再也没有“的、地、得”题目能难倒你了!`,
        },
      ],
    };
  },
  methods: {
    questionAnswered(isCorrect) {
      if (isCorrect) this.totalCorrect++;
      this.questionsAnswered++;
    },
    reset() {
      this.questionsAnswered = 0;
      this.totalCorrect = 0;
    },
  },
};
</script>

<style></style>
