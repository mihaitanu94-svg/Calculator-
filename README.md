
<                    <input type="number" class="p-buc" value="0">
                </div>
                <div class="input-group" style="flex: 0.5;">
                    <label>Coef.</label>
                    <input type="number" class="p-coef" step="0.01" value="0">
                </div>
                <div class="input-group" style="flex: 0.4;">
                    <label>Pers.<<label>Coeficient</label>
                    <input type="number" class="l-coef" step="0.01" value="0">
                </div>
            </div>
        </div>
        <button class="btn-add" onclick="adaugaRand('lista-lazi', false)" style="background: #6366f1;">+ Adaugă Alt Sort de Lăzi</button>
    </div>

    <button class="btn-calc" onclick="calculeazaTot()">CALCULEAZĂ REZULTAT FINAL</button>

    <div id="rezultat" class="result-area">
        <span style="color: #94a3b8; font-size: 14px;">PUNCTAJ TOTAL:</span>
        <span id="suma" class="total-val">0</span>
        <span style="color: #22d3ee; font-size: 12px; font-weight: bold;">PREMIE CALCULATĂ: 135%</span>
    </div>
</div>

<script>
function adaugaRand(idLista, isFormulaComplex) {
    const container = document.getElementById(idLista);
    const div = document.createElement('div');
    div.className = 'input-row';
    
    if(isFormulaComplex) {
        div.innerHTML = `
            <div class="input-group"><input type="text" class="p-nume" placeholder="Ex: Sortenwechsel"></div>
            <div class="input-group" style="flex: 0.5;"><input type="number" class="p-buc" value="0"></div>
            <div class="input-group" style="flex: 0.5;"><input type="number" class="p-coef" step="0.01" value="0"></div>
            <div class="input-group" style="flex: 0.4;"><input type="number" class="p-pers" value="4"></div>
            <button class="remove-btn" onclick="this.parentElement.remove()">X</button>`;
    } else {
        div.innerHTML = `
            <div class="input-group"><input type="text" class="l-nume" placeholder="Ex: Lăzi Sort 2"></div>
            <div class="input-group"><input type="number" class="l-buc" value="0"></div>
            <div class="input-group"><input type="number" class="l-coef" step="0.01" value="0"></div>
            <button class="remove-btn" onclick="this.parentElement.remove()">X</button>`;
    }
    container.appendChild(div);
}

function calculeazaTot() {
    let total = 0;
    const premie = 1.35;

    // Calcul formula complexa (Produs x Coef x 1.35 x Persoane)
    const prods = document.querySelectorAll('#lista-productie .input-row');
    prods.forEach(row => {
        let buc = parseFloat(row.querySelector('.p-buc').value) || 0;
        let coef = parseFloat(row.querySelector('.p-coef').value) || 0;
        let pers = parseFloat(row.querySelector('.p-pers').value) || 1;
        total += (buc * coef * premie * pers);
    });

    // Calcul lazi (Buc x Coef)
    const lazi = document.querySelectorAll('#lista-lazi .input-row');
    lazi.forEach(row => {
        let buc = parseFloat(row.querySelector('.l-buc').value) || 0;
        let coef = parseFloat(row.querySelector('.l-coef').value) || 0;
        total += (buc * coef);
    });

    document.getElementById('suma').innerText = total.toFixed(2);
    
