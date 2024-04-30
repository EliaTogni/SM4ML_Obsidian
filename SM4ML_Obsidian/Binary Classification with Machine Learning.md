# Binary Classification with Machine Learning
## Neural Networks for classification of chihuahuas and muffins images

I declare that this material, which I now submit for assessment, is entirely my own work and has not been taken from the work of others, save and to the extent that such work has been cited and acknowledged within the text of our work. I understand that plagiarism, collusion, and copying are grave and serious offences in the university and accept the penalties that would be imposed should I engage in plagiarism, collusion or copying. This assignment, or any spart of it, has not been previously submitted by us or any other person for assessment on this or any other course of study.

### Abstract

### Scaletta
- [[Introduction]]
	- [[Introduction#Image Classification problem |Image Classification problem]]
	- [[Introduction#Chihuahua vs Muffins classification |Chihuahua vs Muffins classification]]
	- [[Introduction#Overview |Overview]]
- [[Environment and used tools]]
- [[Chihuahua vs Muffin Dataset]]
	- [[Chihuahua vs Muffin Dataset#Data Organization |Data Organization]]
	- [[Chihuahua vs Muffin Dataset#Methodology |Methodology]]
	- [[Chihuahua vs Muffin Dataset#Dataset Preprocessing |Dataset Preprocessing]]
		- [[Chihuahua vs Muffin Dataset#Images Removal |Images Removal]]
			- [[Chihuahua vs Muffin Dataset#Chihuahua dataset|Chihuahua Dataset]]
			- [[Chihuahua vs Muffin Dataset#Muffin dataset|Muffin Dataset]]
		- [[Chihuahua vs Muffin Dataset#Unbalance Resolution |Unbalance Resolution]]
		- [[Chihuahua vs Muffin Dataset#Image Conversion |Image Conversion]]
			- [[Chihuahua vs Muffin Dataset#RGB |RGB]]
			- [[Chihuahua vs Muffin Dataset#Greyscale |Greyscale]]
		- [[Chihuahua vs Muffin Dataset#Image Cropping |Image Cropping]]
		- [[Chihuahua vs Muffin Dataset#Image Resizing |Image Resizing]]
		- [[Chihuahua vs Muffin Dataset#Data Augmentation |Data Augmentation]]
		- [[Chihuahua vs Muffin Dataset#Image Normalization |Image Normalization]]
		- [[Chihuahua vs Muffin Dataset#Dataset Shuffling |Dataset Shuffling]]
		- [[Chihuahua vs Muffin Dataset#Dataset Splitting |Dataset Splitting]]
			- [[Chihuahua vs Muffin Dataset#Training Set |Training Set]]
			- [[Chihuahua vs Muffin Dataset#Validation Set |Validation Set]]
			- [[Chihuahua vs Muffin Dataset#Testing Set |Testing Set]]
- Experiments
	- Artificial Neural Networks
		- An Introduction to Artificial Neural Networks
		- Multi Level Neural Networks
	- Convolutional Neural Networks
		- An Introduction to Convolutional Neural Networks
		- Inception V3
		- TogNet
- [[Statistical Analysis]]
	- Grad-CAM
- [[Results and Conclusion]]
	- [[Results and Conclusion#Interesting Questions and Observations |Interesting Questions and Observations]]

# To Do List

- [x] Check codice Max cropping ✅ 2024-04-24
- [x] Check codice Rita cropping ✅ 2024-04-24
- [x] Creare repo per papers in base alle sezioni in cui le uso ✅ 2024-04-22
- [x] Kumar bibtex check utilità ✅ 2024-04-22
- [x] Dogs_folder elenco immagini da rimuovere ✅ 2024-04-22
- [x] aggiungere imbalance ration dogs_folder ✅ 2024-04-22
- [ ] immagini 3_16, 3_338, e_334 chihuahua con schiuma GradCAM
- [x] documentazione funzione di cropping (2) ✅ 2024-04-25
- [x] documentazione funzione di padding e resizing (3) ✅ 2024-04-25
- [x] Rileggere paper resizing per scegliere size ✅ 2024-04-24
- [ ] Aggiungere matrice di confusione nella fase di analisi statistica (paper imbalanced data)
- [x] Check se Rita usa interpolation per confrontare con lo zero padding (non lo fa) ✅ 2024-04-24
- [x] Fare dictionary size delle immagini nei dataset ✅ 2024-04-23
- [x] Capire dove inserire codice dictionary ✅ 2024-04-22
- [x] Aggiungere if PREPROCESSING ✅ 2024-04-24
- [x] check with image close() ✅ 2024-04-22
- [x] refactoring img in image ✅ 2024-04-24
- [x] except sizes_freq ✅ 2024-04-24
- [x] Restructuring codice ✅ 2024-04-23
- [x] Check Rita if PREPROCESSING ✅ 2024-04-23
- [x] Clear Drive ✅ 2024-04-23
- [x] Rerun x controllo ✅ 2024-04-23
- [x] Strutturare gerarchia con disegno ✅ 2024-04-23
- [x] Stabilire dove mettere preprocessing ✅ 2024-04-24
- [x] Ristrutturare codice per generare MODIFIED DATASET ✅ 2024-04-24
- [x] Printare dictionary taglie + exceptions ✅ 2024-04-24
- [x] Check codice Max definizione funzioni ✅ 2024-04-24
- [x] chatgpt try with python ✅ 2024-04-24
- [x] ImageChops (2) ✅ 2024-04-24
- [ ] Motivare il bbox crop dopo rgb/grey
- [x] Fixare zero padding (1) ✅ 2024-04-25
- [x] check if nuovo metodo modifica immagini ✅ 2024-04-24
- [ ] aggiungere tuple output funzioni
- [x] leggere paper augmentation ✅ 2024-04-26
- [x] Rifrasare image cropping spiegazione (3) ✅ 2024-04-27
- [x] Scelta augmentation  ✅ 2024-04-26
- [x] Chiedere a chat gpt quanti tipi di augmentation ci sono ✅ 2024-04-26
- [x] Chiedere a chatgpt di classificare le varie augmentation ✅ 2024-04-26
- [ ] leggere paper segmentation (7)
- [x] Aggiornare report con modifiche finora ✅ 2024-04-26
- [ ] Check codice max augmentation 
- [ ] Check paper rita augmentation (5)
- [x] fixare parentesi muffin image removal ✅ 2024-04-27
- [x] chagpt global quantities frasca ✅ 2024-04-28
- [ ] Scelta tipi augmentation (8/10 tipi 25%) rotation, scaling, mirroring, contrast, brightness, blurring, unsharpening, ... (3)
- [ ] Finire sistemare fino a data augmentation (4)
- [ ] Rifrasare parte finale image resizing (2)
- [x] aggiungere simbolo gradi rotation geometric transformation ✅ 2024-04-27
- [ ] Leggere paper max segmentation (6)
- [ ] Aggiunta segmentation obsidian (8)
- [ ] Giustificare normalization (10)
- [ ] Chech normalization paper kidara (9)
- [ ] Check cite shorten data augmentation (0)
- [x] Check overleaf bibtex shorten (1) ✅ 2024-04-30