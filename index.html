<!doctype html>

<html lang="en">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>TIYUMBA MA Primary — School-Based Assessment (GES)</title>
  <!-- Tailwind CSS -->
  <script src="https://cdn.tailwindcss.com"></script>
  <meta name="description" content="GES-aligned School-Based Assessment app for TIYUMBA MA Primary. Record marks, auto-calc totals, generate report cards, batch print, and share via SMS/WhatsApp." />
  <style>
    /* Print styles: one report per page */
    @media print {
      .no-print { display: none !important; }
      .report-card { page-break-after: always; }
      body { background: white; }
    }
  </style>
</head>
<body class="bg-slate-50 text-slate-900">
  <div id="root"></div>  <!-- React 18 + ReactDOM -->  <script src="https://unpkg.com/react@18/umd/react.production.min.js"></script>  <script src="https://unpkg.com/react-dom@18/umd/react-dom.production.min.js"></script>  <!-- Babel for inline JSX (works on Vercel as a static site). For production bundling, replace with a build step. -->  <script src="https://unpkg.com/@babel/standalone/babel.min.js"></script>  <script type="text/babel">
    const { useState, useMemo, useEffect } = React;

    /******************** CONFIG ********************/
    const SUBJECTS = [
      'Mathematics','English','Science','Our World Our People (OWOP)',
      'Computing','Creative Arts','French','Ghanaian Language'
    ];

    const DEFAULT_TERM = {
      academicYear: new Date().getFullYear() + "/" + (new Date().getFullYear()+1),
      term: 'Term 1',
      totalSchoolDays: 25,
      schoolName: 'TIYUMBA MA PRIMARY SCHOOL',
      headTeacher: '—',
      className: 'BASIC 6',
    };

    // Auto-remark by total score (0-100)
    function remarkForScore(total){
      if(total >= 85) return 'Excellent performance. Keep it up!';
      if(total >= 70) return 'Very good work. Maintain the effort.';
      if(total >= 60) return 'Good. Aim higher next term.';
      if(total >= 50) return 'Credit. More practice needed.';
      if(total >= 40) return 'Pass. Work harder to improve.';
      return 'Below average. Serious improvement required.';
    }

    function scaleExamTo50(examRaw){
      const n = Number(examRaw || 0);
      return Math.round((n / 100) * 50);
    }

    function continuousAssessment(ct1, ct2, ct3, project){
      const s = Number(ct1||0) + Number(ct2||0) + Number(ct3||0) + Number(project||0);
      return Math.max(0, Math.min(50, s));
    }

    function finalTotal(ca50, exam50){
      return Math.max(0, Math.min(100, Number(ca50||0) + Number(exam50||0)));
    }

    function denseRank(values){
      // values: array of numbers (higher is better)
      const sortedUniqueDesc = Array.from(new Set(values.slice().sort((a,b)=>b-a)));
      const map = new Map(sortedUniqueDesc.map((v,i)=>[v,i+1]));
      return values.map(v => map.get(v));
    }

    /******************** STORAGE ********************/
    const LS_KEY = 'tiyumba-sba-v1';
    function loadState(){
      try{ return JSON.parse(localStorage.getItem(LS_KEY)) || null; }catch{ return null; }
    }
    function saveState(state){
      localStorage.setItem(LS_KEY, JSON.stringify(state));
    }

    /******************** APP ********************/
    function App(){
      const [students, setStudents] = useState(()=>loadState()?.students || []); // [{id, name, gender, parentPhone}]
      const [scores, setScores] = useState(()=>loadState()?.scores || {}); // { studentId: { subjectName: { ct1, ct2, ct3, project, examRaw, attendancePresent } } }
      const [termInfo, setTermInfo] = useState(()=>loadState()?.termInfo || DEFAULT_TERM);
      const [activeTab, setActiveTab] = useState('Scores');

      useEffect(()=>{ saveState({students, scores, termInfo}); }, [students, scores, termInfo]);

      const numberOnRoll = students.length;

      const computed = useMemo(()=>{
        // Build per-student aggregates
        return students.map(stu => {
          let totalAllSubjects = 0;
          let perSubject = {};
          SUBJECTS.forEach(sub => {
            const rec = scores?.[stu.id]?.[sub] || {};
            const ca = continuousAssessment(rec.ct1, rec.ct2, rec.ct3, rec.project);
            const exam50 = scaleExamTo50(rec.examRaw);
            const total = finalTotal(ca, exam50);
            perSubject[sub] = { ca, exam50, total };
            totalAllSubjects += total;
          });
          const avg = SUBJECTS.length ? Math.round((totalAllSubjects / SUBJECTS.length) * 10) / 10 : 0; // 1 dp
          return { stu, perSubject, totalAllSubjects, avg };
        });
      }, [students, scores]);

      // Class position by average
      const avgs = computed.map(x=>x.avg);
      const positions = denseRank(avgs);

      return (
        <div className="max-w-7xl mx-auto p-4">
          <header className="no-print bg-white rounded-2xl shadow p-4 mb-4">
            <div className="flex flex-col gap-2 md:flex-row md:items-center md:justify-between">
              <h1 className="text-2xl font-bold">{termInfo.schoolName} — SBA (GES)</h1>
              <div className="flex flex-wrap gap-2">
                {['Scores','Students','Reports','Settings','Help'].map(tab => (
                  <button key={tab} onClick={()=>setActiveTab(tab)}
                    className={`px-3 py-2 rounded-xl text-sm font-semibold border ${activeTab===tab?'bg-slate-900 text-white':'bg-white hover:bg-slate-100'}`}>
                    {tab}
                  </button>
                ))}
                <button onClick={()=>window.print()} className="px-3 py-2 rounded-xl text-sm font-semibold border bg-emerald-600 text-white hover:bg-emerald-700">Print All Reports</button>
              </div>
            </div>
          </header>

          {activeTab === 'Settings' && (
            <Settings termInfo={termInfo} setTermInfo={setTermInfo} />
          )}

          {activeTab === 'Students' && (
            <StudentsPage students={students} setStudents={setStudents} scores={scores} setScores={setScores} />
          )}

          {activeTab === 'Scores' && (
            <ScoresPage students={students} scores={scores} setScores={setScores} termInfo={termInfo} />
          )}

          {activeTab === 'Reports' && (
            <ReportsPage students={students} scores={scores} termInfo={termInfo} numberOnRoll={numberOnRoll} positions={positions} computed={computed} />
          )}

          {activeTab === 'Help' && (
            <Help />
          )}

          <footer className="no-print text-center text-xs text-slate-500 mt-8">
            <p>Data is stored locally in your browser. You can export/import from the Students tab.</p>
          </footer>
        </div>
      );
    }

    function Settings({termInfo, setTermInfo}){
      const [form, setForm] = useState(termInfo);
      useEffect(()=>setForm(termInfo), [termInfo]);
      function update(k,v){ setForm(prev=>({...prev,[k]:v})); }
      return (
        <div className="bg-white rounded-2xl shadow p-4">
          <h2 className="text-lg font-bold mb-3">Term & School Settings</h2>
          <div className="grid md:grid-cols-2 gap-4">
            <LabeledInput label="School Name" value={form.schoolName} onChange={e=>update('schoolName', e.target.value)} />
            <LabeledInput label="Class Name" value={form.className} onChange={e=>update('className', e.target.value)} placeholder="e.g., BASIC 6" />
            <LabeledInput label="Academic Year" value={form.academicYear} onChange={e=>update('academicYear', e.target.value)} placeholder="2024/2025" />
            <Select label="Term" value={form.term} onChange={e=>update('term', e.target.value)} options={["Term 1","Term 2","Term 3"]} />
            <NumberInput label="Total School Days in Term" value={form.totalSchoolDays} onChange={v=>update('totalSchoolDays', v)} min={1} max={120} />
            <LabeledInput label="Head Teacher" value={form.headTeacher} onChange={e=>update('headTeacher', e.target.value)} />
          </div>
          <div className="mt-4 flex gap-2">
            <button className="px-4 py-2 rounded-xl bg-slate-900 text-white" onClick={()=>setTermInfo(form)}>Save Settings</button>
          </div>
        </div>
      );
    }

    function StudentsPage({students, setStudents, scores, setScores}){
      const [name, setName] = useState('');
      const [gender, setGender] = useState('Female');
      const [parentPhone, setParentPhone] = useState('');

      function addStudent(){
        const trimmed = name.trim();
        if(!trimmed) return;
        const id = crypto.randomUUID();
        const newStu = {id, name: trimmed, gender, parentPhone};
        setStudents(prev=>[...prev, newStu]);
        setName(''); setParentPhone('');
      }

      function removeStudent(id){
        if(!confirm('Remove this pupil?')) return;
        setStudents(prev=>prev.filter(s=>s.id!==id));
        const s2 = {...scores};
        delete s2[id];
        setScores(s2);
      }

      function exportData(){
        const blob = new Blob([JSON.stringify({students, scores}, null, 2)], {type:'application/json'});
        const url = URL.createObjectURL(blob);
        const a = document.createElement('a');
        a.href = url; a.download = 'tiyumba-sba-data.json'; a.click();
        URL.revokeObjectURL(url);
      }

      function importData(e){
        const file = e.target.files?.[0];
        if(!file) return;
        const reader = new FileReader();
        reader.onload = (ev)=>{
          try{
            const obj = JSON.parse(ev.target.result);
            if(obj.students && obj.scores){
              setStudents(obj.students);
              setScores(obj.scores);
              alert('Import successful.');
            } else {
              alert('Invalid file.');
            }
          }catch(err){ alert('Failed to parse file.'); }
        };
        reader.readAsText(file);
      }

      return (
        <div className="bg-white rounded-2xl shadow p-4">
          <h2 className="text-lg font-bold mb-3">Pupils</h2>
          <div className="grid md:grid-cols-4 gap-3">
            <LabeledInput label="Full Name" value={name} onChange={e=>setName(e.target.value)} placeholder="e.g., Abena Mensah" />
            <Select label="Gender" value={gender} onChange={e=>setGender(e.target.value)} options={["Female","Male"]} />
            <LabeledInput label="Parent's Phone" value={parentPhone} onChange={e=>setParentPhone(e.target.value)} placeholder="e.g., 024XXXXXXX" />
            <div className="flex items-end">
              <button className="w-full px-4 py-2 rounded-xl bg-emerald-600 text-white" onClick={addStudent}>Add Pupil</button>
            </div>
          </div>

          <div className="mt-4 overflow-x-auto">
            <table className="min-w-full text-sm">
              <thead>
                <tr className="bg-slate-100">
                  <th className="text-left p-2">#</th>
                  <th className="text-left p-2">Name</th>
                  <th className="text-left p-2">Gender</th>
                  <th className="text-left p-2">Parent Phone</th>
                  <th className="text-left p-2">Actions</th>
                </tr>
              </thead>
              <tbody>
                {students.map((s, i)=> (
                  <tr key={s.id} className="border-b">
                    <td className="p-2">{i+1}</td>
                    <td className="p-2">{s.name}</td>
                    <td className="p-2">{s.gender}</td>
                    <td className="p-2">{s.parentPhone}</td>
                    <td className="p-2">
                      <button className="px-3 py-1 rounded-lg bg-red-600 text-white" onClick={()=>removeStudent(s.id)}>Remove</button>
                    </td>
                  </tr>
                ))}
                {students.length===0 && (
                  <tr><td colSpan="5" className="p-3 text-slate-500">No pupils yet. Add pupils using the form above.</td></tr>
                )}
              </tbody>
            </table>
          </div>

          <div className="mt-4 flex flex-wrap gap-2">
            <button className="px-4 py-2 rounded-xl bg-slate-900 text-white" onClick={exportData}>Export Data</button>
            <label className="px-4 py-2 rounded-xl bg-slate-200 cursor-pointer">
              Import Data
              <input type="file" accept="application/json" className="hidden" onChange={importData} />
            </label>
          </div>
        </div>
      );
    }

    function ScoresPage({students, scores, setScores, termInfo}){
      const [activeSubject, setActiveSubject] = useState(SUBJECTS[0]);

      function update(studentId, field, value){
        setScores(prev => {
          const copy = {...prev};
          copy[studentId] = copy[studentId] || {};
          copy[studentId][activeSubject] = copy[studentId][activeSubject] || {};
          copy[studentId][activeSubject][field] = value;
          return copy;
        });
      }

      function updateAttendance(studentId, present){
        setScores(prev => {
          const copy = {...prev};
          copy[studentId] = copy[studentId] || {};
          copy[studentId]['__attendance'] = { present: present, total: termInfo.totalSchoolDays };
          return copy;
        });
      }

      return (
        <div className="bg-white rounded-2xl shadow p-4">
          <div className="flex flex-wrap items-center gap-2 mb-3">
            <h2 className="text-lg font-bold">Record Scores</h2>
            <span className="text-sm text-slate-500">Term: {termInfo.term} • Year: {termInfo.academicYear} • Class: {termInfo.className}</span>
          </div>

          <div className="no-print flex flex-wrap gap-2 mb-3">
            {SUBJECTS.map(s => (
              <button key={s} onClick={()=>setActiveSubject(s)} className={`px-3 py-2 rounded-xl text-sm border ${activeSubject===s?'bg-slate-900 text-white':'bg-white hover:bg-slate-100'}`}>{s}</button>
            ))}
          </div>

          <div className="overflow-x-auto">
            <table className="min-w-full text-sm">
              <thead>
                <tr className="bg-slate-100">
                  <th className="text-left p-2">#</th>
                  <th className="text-left p-2">Pupil</th>
                  <th className="text-left p-2">CT1 /10</th>
                  <th className="text-left p-2">CT2 /10</th>
                  <th className="text-left p-2">CT3 /10</th>
                  <th className="text-left p-2">Project /20</th>
                  <th className="text-left p-2">CA /50</th>
                  <th className="text-left p-2">Exam Raw /100</th>
                  <th className="text-left p-2">Exam /50</th>
                  <th className="text-left p-2">Total /100</th>
                  <th className="text-left p-2">Attendance</th>
                </tr>
              </thead>
              <tbody>
                {students.map((stu, i)=>{
                  const rec = scores?.[stu.id]?.[activeSubject] || {};
                  const ca = continuousAssessment(rec.ct1, rec.ct2, rec.ct3, rec.project);
                  const exam50 = scaleExamTo50(rec.examRaw);
                  const total = finalTotal(ca, exam50);
                  const att = scores?.[stu.id]?.['__attendance'] || {present: '', total: termInfo.totalSchoolDays};
                  return (
                    <tr key={stu.id} className="border-b">
                      <td className="p-2">{i+1}</td>
                      <td className="p-2">{stu.name}</td>
                      <td className="p-2"><MarkInput max={10} value={rec.ct1} onChange={v=>update(stu.id,'ct1',v)} /></td>
                      <td className="p-2"><MarkInput max={10} value={rec.ct2} onChange={v=>update(stu.id,'ct2',v)} /></td>
                      <td className="p-2"><MarkInput max={10} value={rec.ct3} onChange={v=>update(stu.id,'ct3',v)} /></td>
                      <td className="p-2"><MarkInput max={20} value={rec.project} onChange={v=>update(stu.id,'project',v)} /></td>
                      <td className="p-2 font-semibold">{ca}</td>
                      <td className="p-2"><MarkInput max={100} value={rec.examRaw} onChange={v=>update(stu.id,'examRaw',v)} /></td>
                      <td className="p-2 font-semibold">{exam50}</td>
                      <td className="p-2 font-bold">{total}</td>
                      <td className="p-2">
                        <div className="flex items-center gap-1">
                          <input type="number" className="w-20 rounded-lg border p-1" placeholder="Present" value={att.present}
                            onChange={e=>updateAttendance(stu.id, Number(e.target.value))} min={0} max={termInfo.totalSchoolDays} />
                          <span className="text-xs text-slate-500">/ {termInfo.totalSchoolDays}</span>
                        </div>
                      </td>
                    </tr>
                  );
                })}
                {students.length===0 && (
                  <tr><td colSpan="11" className="p-3 text-slate-500">Add pupils first from the Students tab.</td></tr>
                )}
              </tbody>
            </table>
          </div>
        </div>
      );
    }

    function ReportsPage({students, scores, termInfo, numberOnRoll, positions, computed}){
      if(students.length===0) return (
        <div className="bg-white rounded-2xl shadow p-4">
          <p className="text-slate-500">No pupils yet. Add pupils from the Students tab.</p>
        </div>
      );

      return (
        <div className="space-y-6">
          {students.map((stu, idx)=>{
            const att = scores?.[stu.id]?.['__attendance'] || {present: '', total: termInfo.totalSchoolDays};
            const perf = computed[idx];
            const position = positions[idx];
            return (
              <div key={stu.id} className="report-card bg-white rounded-2xl shadow p-4">
                <div className="flex flex-col md:flex-row md:items-center md:justify-between">
                  <div>
                    <h3 className="text-xl font-bold">{termInfo.schoolName}</h3>
                    <p className="text-sm text-slate-600">GES Report Card • {termInfo.academicYear} • {termInfo.term} • {termInfo.className}</p>
                  </div>
                  <div className="mt-2 md:mt-0 text-sm text-slate-600">
                    <p><span className="font-semibold">Head Teacher:</span> {termInfo.headTeacher || '—'}</p>
                  </div>
                </div>
                <hr className="my-3"/>

                <div className="grid md:grid-cols-2 gap-2 text-sm">
                  <p><span className="font-semibold">Pupil:</span> {stu.name}</p>
                  <p><span className="font-semibold">Gender:</span> {stu.gender}</p>
                  <p><span className="font-semibold">Attendance:</span> {att.present || 0}/{att.total}</p>
                  <p><span className="font-semibold">No. on Roll:</span> {numberOnRoll}</p>
                  <p><span className="font-semibold">Position:</span> {position}{ordinalSuffix(position)}</p>
                  <p><span className="font-semibold">Parent Contact:</span> {stu.parentPhone || '—'}</p>
                </div>

                <div className="overflow-x-auto mt-3">
                  <table className="min-w-full text-sm">
                    <thead>
                      <tr className="bg-slate-100">
                        <th className="text-left p-2">Subject</th>
                        <th className="text-left p-2">Class Tests + Project (50)</th>
                        <th className="text-left p-2">Exam (50)</th>
                        <th className="text-left p-2">Total (100)</th>
                      </tr>
                    </thead>
                    <tbody>
                      {SUBJECTS.map(sub=>{
                        const rec = scores?.[stu.id]?.[sub] || {};
           
