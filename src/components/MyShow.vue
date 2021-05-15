<script>
import { h, ref } from "@vue/runtime-core";
export default {
  setup() {
    let inputValue = ref(null);
    let shows = ref([]);
    let error = ref(null);

    const searchText = async (search) => {
      console.log("searchText", search);
      if (!search) return;
      shows.value = [];
      const result = await fetch(
        `http://api.tvmaze.com/search/shows?q=${search}`
      ).catch((e) => {
        error.value = "error" + e;
        console.log("got an error", error.value);
        return;
      });
      shows.value = await result.json().catch((e) => (error.value = e));
    };
    return () => {
      return h(
        "form",
        {
          style: "color: red; margin: auto",
          class: "form",
          onSubmit: (event) => event.preventDefault(),
        },
        [
          h("input", {
            onInput: (event) => {
              inputValue.value = event.target.value;
            },
            class: "search",
          }),
          h(
            "button",
            {
              onClick: () => {
                searchText(inputValue.value);
              },
              class: "button",
            },
            "Press Me"
          ),
          h("div", { class: "shows" }, [
            error.value
              ? h("div", error.value)
              : shows.value.map((show) => {
                  console.log(show);
                  return h("div", { class: "show" }, [
                    h("img", { src: show.show.image?.medium }),
                    h("div", { class: "title" }, show.show.name),
                  ]);
                }),
          ]),
        ]
      );
    };
  },
};
</script>
<style scoped>
.form {
    display: flex;
    flex-wrap: wrap;
    justify-content: center;
    max-width: 800px;
}

.shows {
  padding-top: 20px;
  display: flex;
  flex-wrap: wrap;
  justify-content: space-between;
  width: 100%;
}

.show {
  /* margin: 20px; */
  width: 30%;
}

.title {
  padding-top: 10px;
  padding-bottom: 20px;
}

.search {
  padding: 10px;
  font-size: 17px;
  border: 1px solid grey;
  float: left;
  width: 60%;
  background: #f1f1f1;
}

.button {
  float: left;
  width: 15%;
  padding: 10px;
  background: #2196f3;
  color: white;
  font-size: 17px;
  border: 1px solid grey;
  border-left: none; /* Prevent double borders */
  cursor: pointer;
}
</style>>