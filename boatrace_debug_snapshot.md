# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-08-15T17:50:01.982168+09:00

### 次に取るべきアクション
> RED最優先: CIRCUIT_BREAKER_TRIP×53 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×96 (24h)
- 🔴 CIRCUIT_BREAKER_TRIP×53 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🔴 CALIBRATION_DRIFT×8 (24h)
- 🟡 LARGE_ODDS_DRIFT×1 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 CIRCUIT_BREAKER_TRIP  ×129  [2026-08-15T17:07:04]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×129  [2026-08-15T17:07:04]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 STRATEGY_CI_FAIL  ×43  [2026-08-15T17:07:04]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×2  [2026-08-15T17:00:03]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S00 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×2  [2026-08-15T17:00:03]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S01_NAKAANA1 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×2  [2026-08-15T17:00:03]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S02_TETSUBAN が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CALIBRATION_DRIFT  ×36  [2026-08-15T16:27:05]
- key: `CALIBRATION_DRIFT|`
- **FIX**: 予測確率が実的中率から50%以上乖離→isotonic_calibration.json 再生成 or モデル再学習が必要。EV計算が膨張中

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×9  [2026-08-15T14:24:39]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×10  [2026-08-15T12:51:39]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### 🟡 ANOMALY_BET_VOLUME_DROP  ×38  [2026-08-15T11:00:30]
- key: `ANOMALY_BET_VOLUME_DROP|`
- **FIX**: 本日のbet数が7日baselineから2σ低下。戦略filter/ scan fix/run_cycle停止を疑え

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-08-15T06:00:09]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=72<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-08-15T06:00:09]
- key: `INSUFFICIENT_SAMPLE|S00: n=174<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-08-15T06:00:09]
- key: `ROI_STAT|S00: n=174 hit%=21.8% hit_CI[Bonf]=[14.2,32.1]% ROI=0.62 ROI_boot95=[0.42,0.84]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-08-15T06:00:09]
- key: `ROI_STAT|S01_NAKAANA1: n=168 hit%=20.2% hit_CI[Bonf]=[12.8,30.5]% ROI=0.64 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-08-15T06:00:09]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=168<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-08-15T06:00:09]
- key: `ROI_STAT|S02_TETSUBAN: n=72 hit%=54.2% hit_CI[Bonf]=[37.7,69.8]% ROI=0.90 ROI_boot95=[0.6`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### 🟡 ORPHAN_SCAN  ×1  [2026-08-15T06:00:09]
- key: `ORPHAN_SCAN|194 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ DRIFT_BUCKET  ×1  [2026-08-15T06:00:09]
- key: `DRIFT_BUCKET|drift ≤-30%: n=39 hit%=20.5% ROI=0.60 (コスト 11,200/回収 6,770)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-08-15T06:00:09]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=35 hit%=34.3% ROI=0.99 (コスト 8,500/回収 8,450)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-08-15T06:00:09]
- key: `DRIFT_BUCKET|drift -10%〜+10%: n=70 hit%=25.7% ROI=0.58 (コスト 16,500/回収 9,650)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 10.64MB / last modified 2026-08-15T17:49:58.046336+09:00

### データファイル存在確認
| file | exists | md5 | size |
|---|---|---|---|
| lgbm_model_top1.txt | True | `5b55d55bdb59df95ccfd1745d4e9b469` | 769682 |
| lgbm_model_top3.txt | True | `d5fd8d8393fd859ed913813abbf60084` | 969111 |
| calibration_v7.json | True | `1c04ab3c1a1f074da889e6f5f06adbf3` | 1450 |
| pl_corr_v8_final.json | True | `8727224dfcc3d7548845e2e41caef7be` | 1209 |

### crontab
```
# boatrace_v2 - managed by めう/Claude
SHELL=/bin/bash
PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin

# 1分毎: 統合サイクル (run_cycle.py, flock で並行実行防止)
* 8-23 * * * cd /opt/boatrace_v2 && flock -n /var/lock/run_cycle.lock /opt/boatrace/venv/bin/python3 run_cycle.py >> logs/run_cycle.log 2>&1

# 10分毎: pending alert flush
*/10 * * * * cd /opt/boatrace_v2 && /opt/boatrace/venv/bin/python3 dispatch_pending.py >> logs/dispatch.log 2>&1

# 10分毎: snapshot 生成 + GitHub 同期 (Claude 次セッション用)
*/10 * * * * cd /opt/boatrace_v2 && bash sync_snapshot_to_github.sh >> logs/sync_snapshot.log 2>&1

# 5分毎: 結果取得
*/5 * * * * cd /opt/boatrace_v2 && /opt/boatrace/venv/bin/python3 record_results.py >> logs/results.log 2>&1

# 30分毎: health check
*/30 * * * * cd /opt/boatrace_v2 && /opt/boatrace/venv/bin/python3 health.py >> logs/health.log 2>&1

# 6時: 日次総合検査
0 6 * * *  cd /opt/boatrace_v2 && /opt/boatrace/venv/bin/python3 verify_all.py >> logs/verify_all.log 2>&1

# 0時: 日次集計
5 0 * * *  cd /opt/boatrace_v2 && /opt/boatrace/venv/bin/python3 daily_summary.py >> logs/daily.log 2>&1
0 3 * * * find /opt -maxdepth 1 -name "boatrace_v2.bak_*" -mtime +7 -exec rm -rf {} \; # backup cleanup

# 30分毎: コード/DB a
```

### 直近 run_cycle ログ (末尾)
```
d=20260815: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 3s
2026-08-15 17:49:40,636 [INFO] scraper: odds3t: 120/120 parsed
2026-08-15 17:49:41,711 [INFO] scraper: odds3f: 20/20 parsed
2026-08-15 17:49:42,819 [INFO] scraper: odds2t: 30/30 parsed
2026-08-15 17:49:42,821 [INFO] scraper: odds2f: 15/15 parsed
2026-08-15 17:49:43,932 [INFO] scraper: odds_win: 6/6 parsed
2026-08-15 17:49:43,933 [INFO] scraper: fetch_race 01/7: boats=6 odds=191/191
2026-08-15 17:49:43,936 [INFO] predictor: CALIBRATION_MODE=on
2026-08-15 17:49:43,936 [INFO] predictor: combos: {'win': 6, '2t': 30, '3t': 120}
2026-08-15 17:49:43,940 [INFO] run_cycle: fetched 01/7 [final]: 156 combos
2026-08-15 17:49:47,411 [INFO] scraper: odds3t: 120/120 parsed
2026-08-15 17:49:48,510 [INFO] scraper: odds3f: 20/20 parsed
2026-08-15 17:49:49,588 [INFO] scraper: odds2t: 30/30 parsed
2026-08-15 17:49:49,589 [INFO] scraper: odds2f: 15/15 parsed
2026-08-15 17:49:50,669 [INFO] scraper: odds_win: 6/6 parsed
2026-08-15 17:49:50,669 [INFO] scraper: fetch_race 22/12: boats=6 odds=191/191
2026-08-15 17:49:50,671 [INFO] predictor: CALIBRATION_MODE=on
2026-08-15 17:49:50,671 [INFO] predictor: combos: {'win': 6, '2t': 30, '3t': 120}
2026-08-15 17:49:50,676 [INFO] run_cycle: fetched 22/12 [scan]: 156 combos
2026-08-15 17:49:54,187 [INFO] scraper: odds3t: 120/120 parsed
2026-08-15 17:49:55,298 [INFO] scraper: odds3f: 20/20 parsed
2026-08-15 17:49:56,404 [INFO] scraper: odds2t: 30/30 parsed
2026-08-15 17:49:56,405 [INFO] scraper: odds2f: 15/15 parsed
2026-08-15 17:49:57,515 [INFO] scraper: odds_win: 6/6 parsed
2026-08-15 17:49:57,515 [INFO] scraper: fetch_race 12/7: boats=6 odds=191/191
2026-08-15 17:49:57,518 [INFO] predictor: CALIBRATION_MODE=on
2026-08-15 17:49:57,518 [INFO] predictor: combos: {'win': 6, '2t': 30, '3t': 120}
2026-08-15 17:49:57,523 [INFO] run_cycle: fetched 12/7 [scan]: 156 combos
2026-08-15 17:49:57,652 [INFO] run_cycle: run_cycle done: 0 notifications

```

## 戦略有効/無効一覧
| id | trust | bt | ev_th | pmin | enabled |
|---|---|---|---|---|---|
| S00 | S | win | 4.0 | 0.0 | True |
| S01_NAKAANA1 | A | win | 1.5 | 0.0 | True |
| S02_TETSUBAN | A | win | 1.0 | 0.0 | True |
| S03_NAKAANA4 | B | win | 1.0 | 0.0 | False |
| S04_SELL_3T | B | 3t | 1.0 | 0.0 | False |
| S05_2T_MANKEN | B | 2t | 1.0 | 0.0 | False |
| S06_2F_AXIS1 | B | 2f | 1.0 | 0.0 | False |
| S07_2T_HONMEI | B | 2t | 1.0 | 0.0 | False |

## Webhook送信 (24h)
```
[
  {
    "target": "mirror",
    "ok": 1,
    "c": 94
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 94
  }
]
```

## Phase別通知記録 (24h)
{'final': 34, 'result': 16, 'scan': 44}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 126
  FINAL_MISSING: 96
  CIRCUIT_BREAKER_TRIP: 53
  CIRCUIT_BREAKER_NO_ACTION: 51
  STRATEGY_CI_FAIL: 17
  ANOMALY_SCAN_FINAL_RATIO: 8
  CALIBRATION_DRIFT: 8
  ANOMALY_BET_VOLUME_DROP: 2
  LARGE_ODDS_DRIFT: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 47 | 11 | 14,100 | 9,330 | -4,770 | 0.662 |
| S01_NAKAANA1 | 52 | 8 | 10,400 | 5,800 | -4,600 | 0.558 |
| S02_TETSUBAN | 22 | 10 | 4,400 | 2,800 | -1,600 | 0.636 |

## 直近アラート (24h・新しい順)
```
[17:48:04] FINAL_MISSING: {"deadline": "2026-08-15T15:16:00+09:00", "kind": "FINAL_MISSING", "nid": "2026081512011516", "sid": "S00"}
[17:41:04] FINAL_MISSING: {"deadline": "2026-08-15T12:09:00+09:00", "kind": "FINAL_MISSING", "nid": "2026081518081209", "sid": "S00"}
[17:35:20] FINAL_MISSING: {"deadline": "2026-08-15T14:04:00+09:00", "kind": "FINAL_MISSING", "nid": "2026081505061404", "sid": "S00"}
[17:35:20] FINAL_MISSING: {"deadline": "2026-08-15T13:04:00+09:00", "kind": "FINAL_MISSING", "nid": "2026081505041304", "sid": "S00"}
[17:23:43] CIRCUIT_BREAKER_TRIP: {"cost": 4400, "kind": "CIRCUIT_BREAKER_TRIP", "n": 22, "payout": 2800, "roi_7d": 0.636, "sid": "S02_TETSUBAN"}
[17:20:17] FINAL_MISSING: {"deadline": "2026-08-15T14:48:00+09:00", "kind": "FINAL_MISSING", "nid": "2026081502091448", "sid": "S00"}
[17:18:26] FINAL_MISSING: {"deadline": "2026-08-15T11:45:00+09:00", "kind": "FINAL_MISSING", "nid": "2026081502031145", "sid": "S00"}
[17:12:28] FINAL_MISSING: {"deadline": "2026-08-15T12:39:00+09:00", "kind": "FINAL_MISSING", "nid": "2026081508051239", "sid": "S00"}
[17:09:26] FINAL_MISSING: {"deadline": "2026-08-15T15:38:00+09:00", "kind": "FINAL_MISSING", "nid": "2026081512021538", "sid": "S00"}
[17:07:03] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
```

## 本日残レース: 36件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 216件 登録 / 180件 締切済
- 通知発射: scan=37 nid / final=31 nid / result=16 nid
- predictions: 16 / うち結果DB記録済: 16
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 13件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S01_NAKAANA1 | 014R | win | 1 | 0.5123 | 4.3 | 2.20 | 200 | scan=4.7 drift=-8.5% | 16:31:18 |
| S01_NAKAANA1 | 013R | win | 1 | 0.5334 | 3.8 | 2.03 | 200 | scan=3.0 drift=+26.7% | 16:05:18 |
| S02_TETSUBAN | 072R | win | 1 | 0.5123 | 2.0 | 1.02 | 200 | scan=- drift=- | 15:48:18 |
| S00 | 012R | win | 1 | 0.5891 | 4.1 | 2.42 | 300 | scan=- drift=- | 15:39:44 |
| S01_NAKAANA1 | 046R | win | 1 | 0.5334 | 4.3 | 2.29 | 200 | scan=4.2 drift=+2.4% | 14:23:18 |
| S01_NAKAANA1 | 056R | win | 1 | 0.4936 | 3.4 | 1.68 | 200 | scan=4.1 drift=-17.1% | 14:01:43 |
| S01_NAKAANA1 | 177R | win | 1 | 0.5334 | 4.8 | 2.56 | 200 | scan=3.4 drift=+41.2% | 13:59:19 |
| S02_TETSUBAN | 037R | win | 1 | 0.5735 | 2.2 | 1.26 | 200 | scan=2.2 drift=+0.0% | 13:53:49 |
| S01_NAKAANA1 | 087R | win | 1 | 0.5586 | 3.2 | 1.79 | 200 | scan=3.2 drift=+0.0% | 13:35:19 |
| S01_NAKAANA1 | 026R | win | 1 | 0.4111 | 4.3 | 1.77 | 200 | scan=4.0 drift=+7.5% | 13:11:36 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 76 | +8.7% | -62.9% | +287.7% | 20 | 9 | 43 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 487.7s |
| **Latency** (scan→final max) | 651.1s |
| **Traffic** (notifications 24h) | 94 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 900円 used |
| **Saturation** (S01_NAKAANA1) | 2,000円 used |
| **Saturation** (S02_TETSUBAN) | 600円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 419 | 0.4667 | 0.2601 | +0.2065 | 🟡+44% | 0.2364 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 174 | 0.4180 | 0.2184 | 0.2217 | 🔴-0.30 | 0.616 |
| S01_NAKAANA1 | win | 173 | 0.4905 | 0.2023 | 0.2482 | 🔴-0.54 | 0.656 |
| S02_TETSUBAN | win | 72 | 0.5269 | 0.5000 | 0.2434 | ✅+0.03 | 0.806 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.10-0.15 | 9 | 0.1189 | 0.1111 | ✅+0.0078 |
| 0.15-0.20 | 12 | 0.1827 | 0.0833 | 🔴+0.0994 |
| 0.20-0.30 | 9 | 0.2228 | 0.4444 | 🔴-0.2216 |
| 0.30-0.50 | 159 | 0.4186 | 0.2138 | 🔴+0.2048 |
| 0.50+ | 228 | 0.5418 | 0.3026 | 🔴+0.2392 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 109 | 0.768 |
| win | <5.0 | ✅learned | 185 | 0.736 |
| win | <10.0 | ✅learned | 94 | 0.45 |
| win | <20.0 | ✅learned | 30 | 0.227 |
| win | <50.0 | ⚠️fallback | 7 | 0.1 |
| win | ∞ | ⚠️fallback | 0 | 0.1 |
| 2t | <10.0 | ⚠️fallback | 0 | 0.5 |
| 2t | <30.0 | ⚠️fallback | 0 | 0.35 |
| 2t | ∞ | ⚠️fallback | 0 | 0.25 |
| 3t | <10.0 | ⚠️fallback | 1 | 0.4 |
| 3t | <50.0 | ⚠️fallback | 0 | 0.4 |
| 3t | <200.0 | ⚠️fallback | 0 | 0.3 |
| 3t | ∞ | ⚠️fallback | 0 | 0.2 |
| 2f | <10.0 | ⚠️fallback | 0 | 0.45 |
| 2f | ∞ | ⚠️fallback | 0 | 0.3 |
| 3f | <50.0 | ⚠️fallback | 0 | 0.4 |
| 3f | ∞ | ⚠️fallback | 0 | 0.25 |

---
_auto-generated by claude_snapshot.py at 2026-08-15T17:50:01.982168+09:00_