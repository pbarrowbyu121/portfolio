<template>
  <div id="instructions" class="p-4">
    <div class="font-bold">Instructions:</div>
    <div class="px-4">
      <ol class="list-decimal list-outside">
        <li>Review the 14 images and 5 Bonus images.</li>
        <li>
          Hold each photo up and match it with the background to find the exact
          spot where it was taken.
        </li>
        <li>
          Locate the corresponding square on the map, noting its column (letter)
          and row (number).
        </li>
        <li>
          Enter the column and row combination at
          <a
            href="https://peterbarrow.dev/decoder"
            target="_blank"
            class="text-blue-500"
            >peterbarrow.dev/decoder</a
          >
          to get a decoded letter.
        </li>
        <li>
          Combine and unscramble all decoded letters to reveal the title of one
          of my favorite books. Correct answer is worth 100 points
        </li>
        <li>
          Bonus images have no corresponding letter or message, but are worth 10
          points for finding their location.
        </li>
      </ol>
    </div>
  </div>
</template>

<script>
export default {
  name: 'TreasureHuntInstructions',
}
</script>

<style></style>
