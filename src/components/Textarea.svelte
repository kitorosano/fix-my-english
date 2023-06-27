<script>
  import { checkIsEnglish } from "../services/ia"
  import { isValidInput } from "./store"
  import debounce from "just-debounce-it"

const checkIsEnglishDebounced = debounce(async (value) => {
  const isEnglish = await checkIsEnglish(value)
  isValidInput.set(isEnglish)
}, 300, true)

const handleChange = async (e) => {
  const { value } = e.target
  const isValid = value.length > 0
  if(!isValid)
    return isValidInput.set(false)

  checkIsEnglishDebounced(value)
}


</script>

<textarea class="flex-1 w-full px-4 py-2 text-base text-gray-700 placeholder-gray-400 bg-white border border-gray-300 rounded-lg appearance-none focus:outline-none focus:ring-2 focus:ring-purple-600 focus:border-transparent" 
  on:input={handleChange}
  id="result" 
  placeholder="Enter your english to fix" 
  name="comment" 
  rows="8" 
  cols="40">
</textarea>
