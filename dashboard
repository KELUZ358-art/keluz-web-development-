
const getData = (key) => {
  try {
    return JSON.parse(localStorage.getItem("keluz_" + key)) || [];
  } catch {
    return [];
  }
};

const saveData = (key, data) => {
  localStorage.setItem("keluz_" + key, JSON.stringify(data));
};

let clients = getData("clients");
let projects = getData("projects");
let incomes = getData("incomes");

const money = (amount) =>
  "NLe " + Number(amount || 0).toLocaleString("en-US", {
    minimumFractionDigits: 2,
    maximumFractionDigits: 2
  });

function render() {
  document.getElementById("clientCount").textContent = clients.length;
  document.getElementById("projectCount").textContent = projects.length;

  const total = incomes.reduce(
    (sum, item) => sum + Number(item.amount || 0), 0
  );
  document.getElementById("totalIncome").textContent = money(total);

  document.getElementById("clientList").innerHTML =
    clients.map((c, i) => `
      <div class="record">
        <strong>${escapeHTML(c.name)}</strong>
        <p>${escapeHTML(c.contact || "No contact provided")}</p>
        <button type="button" onclick="deleteClient(${i})">Delete Client</button>
      </div>
    `).join("") || "<p>No clients added yet.</p>";

  document.getElementById("projectList").innerHTML =
    projects.map((p, i) => `
      <div class="record">
        <strong>${escapeHTML(p.name)}</strong>
        <p>Client: ${escapeHTML(p.client || "Not specified")}</p>
        <p>Price: ${money(p.price)}</p>
        <p>Status: ${escapeHTML(p.status)}</p>
        <button type="button" onclick="deleteProject(${i})">Delete Project</button>
      </div>
    `).join("") || "<p>No projects added yet.</p>";

  document.getElementById("incomeList").innerHTML =
    incomes.map((item, i) => `
      <div class="record">
        <strong>${escapeHTML(item.source)}</strong>
        <p>${money(item.amount)}</p>
        <button type="button" onclick="deleteIncome(${i})">Delete Record</button>
      </div>
    `).join("") || "<p>No income recorded yet.</p>";
}

function escapeHTML(value) {
  return String(value).replace(/[&<>"']/g, char => ({
    "&": "&amp;",
    "<": "&lt;",
    ">": "&gt;",
    '"': "&quot;",
    "'": "&#39;"
  })[char]);
}

document.getElementById("clientForm").addEventListener("submit", event => {
  event.preventDefault();

  clients.push({
    name: document.getElementById("clientName").value.trim(),
    contact: document.getElementById("clientContact").value.trim()
  });

  saveData("clients", clients);
  event.target.reset();
  render();
});

document.getElementById("projectForm").addEventListener("submit", event => {
  event.preventDefault();

  projects.push({
    name: document.getElementById("projectName").value.trim(),
    client: document.getElementById("projectClient").value.trim(),
    price: Number(document.getElementById("projectPrice").value),
    status: document.getElementById("projectStatus").value
  });

  saveData("projects", projects);
  event.target.reset();
  render();
});

document.getElementById("incomeForm").addEventListener("submit", event => {
  event.preventDefault();

  incomes.push({
    source: document.getElementById("incomeSource").value.trim(),
    amount: Number(document.getElementById("incomeAmount").value)
  });

  saveData("incomes", incomes);
  event.target.reset();
  render();
});

function deleteClient(index) {
  if (!confirm("Delete this client?")) return;
  clients.splice(index, 1);
  saveData("clients", clients);
  render();
}

function deleteProject(index) {
  if (!confirm("Delete this project?")) return;
  projects.splice(index, 1);
  saveData("projects", projects);
  render();
}

function deleteIncome(index) {
  if (!confirm("Delete this income record?")) return;
  incomes.splice(index, 1);
  saveData("incomes", incomes);
  render();
}

render();
                                 
