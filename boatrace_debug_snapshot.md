# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-10-04T16:20:01.446921+09:00

### 次に取るべきアクション
> RED最優先: STRATEGY_CI_FAIL×17 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×55 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🔴 CIRCUIT_BREAKER_TRIP×12 (24h)
- 🟡 LARGE_ODDS_DRIFT×1 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×9  [2026-10-04T16:10:09]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×22  [2026-10-04T16:07:23]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 STRATEGY_CI_FAIL  ×11  [2026-10-04T16:07:23]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🔴 CIRCUIT_BREAKER_TRIP  ×25  [2026-10-04T15:37:47]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×2  [2026-10-04T15:30:07]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S00 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×2  [2026-10-04T15:30:07]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S02_TETSUBAN が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×14  [2026-10-04T14:52:29]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### 🟡 ANOMALY_BET_VOLUME_DROP  ×42  [2026-10-04T10:00:12]
- key: `ANOMALY_BET_VOLUME_DROP|`
- **FIX**: 本日のbet数が7日baselineから2σ低下。戦略filter/ scan fix/run_cycle停止を疑え

### ℹ️ ROI_STAT  ×1  [2026-10-04T06:02:06]
- key: `ROI_STAT|E2E_TEST_A_IGNORE`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-10-04T06:01:46]
- key: `INSUFFICIENT_SAMPLE|S00: n=164<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-10-04T06:01:46]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=164<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-10-04T06:01:46]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=85<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ CALIBRATION_LIVE  ×1  [2026-10-04T06:01:46]
- key: `CALIBRATION_LIVE|decile 0.05-0.10: n=5 pred=0.0730 actual=0.4000 gap=-0.3270`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ DRIFT_BUCKET  ×1  [2026-10-04T06:01:46]
- key: `DRIFT_BUCKET|drift ≤-30%: n=31 hit%=35.5% ROI=1.00 (コスト 8,700/回収 8,700)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ ROI_STAT  ×1  [2026-10-04T06:01:46]
- key: `ROI_STAT|S00: n=164 hit%=21.3% hit_CI[Bonf]=[13.6,31.8]% ROI=0.61 ROI_boot95=[0.40,0.85]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-10-04T06:01:46]
- key: `ROI_STAT|S01_NAKAANA1: n=164 hit%=27.4% hit_CI[Bonf]=[18.7,38.4]% ROI=0.89 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-10-04T06:01:46]
- key: `ROI_STAT|S02_TETSUBAN: n=85 hit%=47.1% hit_CI[Bonf]=[32.4,62.2]% ROI=0.81 ROI_boot95=[0.6`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### 🟡 ORPHAN_SCAN  ×1  [2026-10-04T06:01:46]
- key: `ORPHAN_SCAN|186 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ DRIFT_BUCKET  ×1  [2026-10-04T06:01:46]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=46 hit%=26.1% ROI=0.67 (コスト 10,600/回収 7,070)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-10-04T06:01:46]
- key: `DRIFT_BUCKET|drift -10%〜+10%: n=89 hit%=27.0% ROI=0.70 (コスト 20,400/回収 14,290)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 14.94MB / last modified 2026-10-04T16:19:08.772964+09:00

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
r: racelist fetch failed: jcd=10 rno=12
2026-10-04 16:18:41,029 [WARNING] run_cycle: fetch None: 10/12
2026-10-04 16:18:52,496 [INFO] scraper: odds3t: 120/120 parsed
2026-10-04 16:18:53,608 [INFO] scraper: odds3f: 20/20 parsed
2026-10-04 16:18:54,695 [INFO] scraper: odds2t: 30/30 parsed
2026-10-04 16:18:54,697 [INFO] scraper: odds2f: 14/15 parsed
2026-10-04 16:18:55,814 [INFO] scraper: odds_win: 5/6 parsed
2026-10-04 16:18:55,814 [INFO] scraper: fetch_race 19/3: boats=6 odds=189/191
2026-10-04 16:18:55,818 [INFO] predictor: CALIBRATION_MODE=on
2026-10-04 16:18:55,818 [INFO] predictor: combos: {'win': 5, '2t': 30, '3t': 120}
2026-10-04 16:18:55,821 [INFO] run_cycle: fetched 19/3 [final]: 155 combos
2026-10-04 16:18:57,607 [INFO] race_id: notif: nid=2026100419031621 sid=S00 phase=final rank=A
2026-10-04 16:18:57,959 [INFO] notifier: Discord notify OK (status=204)
2026-10-04 16:18:58,519 [INFO] notifier: Discord notify OK (status=204)
2026-10-04 16:18:58,616 [INFO] run_cycle: FINAL S00 下関3R A
2026-10-04 16:18:59,085 [INFO] race_id: notif: nid=2026100419031621 sid=S01_NAKAANA1 phase=final rank=A
2026-10-04 16:18:59,502 [INFO] notifier: Discord notify OK (status=204)
2026-10-04 16:18:59,921 [INFO] notifier: Discord notify OK (status=204)
2026-10-04 16:19:00,137 [INFO] run_cycle: FINAL S01_NAKAANA1 下関3R A
2026-10-04 16:19:04,143 [INFO] scraper: odds3t: 120/120 parsed
2026-10-04 16:19:05,279 [INFO] scraper: odds3f: 20/20 parsed
2026-10-04 16:19:06,393 [INFO] scraper: odds2t: 30/30 parsed
2026-10-04 16:19:06,394 [INFO] scraper: odds2f: 15/15 parsed
2026-10-04 16:19:07,464 [INFO] scraper: odds_win: 6/6 parsed
2026-10-04 16:19:07,465 [INFO] scraper: fetch_race 05/12: boats=6 odds=191/191
2026-10-04 16:19:07,467 [INFO] predictor: CALIBRATION_MODE=on
2026-10-04 16:19:07,467 [INFO] predictor: combos: {'win': 6, '2t': 30, '3t': 120}
2026-10-04 16:19:07,471 [INFO] run_cycle: fetched 05/12 [scan]: 156 combos
2026-10-04 16:19:07,855 [INFO] run_cycle: run_cycle done: 2 notifications

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
    "c": 82
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 82
  }
]
```

## Phase別通知記録 (24h)
{'final': 33, 'result': 18, 'scan': 31}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 99
  FINAL_MISSING: 55
  CIRCUIT_BREAKER_NO_ACTION: 35
  STRATEGY_CI_FAIL: 17
  CIRCUIT_BREAKER_TRIP: 12
  ANOMALY_SCAN_FINAL_RATIO: 9
  ANOMALY_BET_VOLUME_DROP: 1
  LARGE_ODDS_DRIFT: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 53 | 12 | 15,900 | 11,100 | -4,800 | 0.698 |
| S01_NAKAANA1 | 49 | 17 | 9,800 | 12,420 | +2,620 | 1.267 |
| S02_TETSUBAN | 17 | 7 | 3,400 | 1,980 | -1,420 | 0.582 |

## 直近アラート (24h・新しい順)
```
[16:19:07] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 4, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1075}
[16:17:39] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1080}
[16:15:46] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1051}
[16:14:05] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1090}
[16:13:39] FINAL_MISSING: {"deadline": "2026-10-04T11:41:00+09:00", "kind": "FINAL_MISSING", "nid": "2026100405031141", "sid": "S00"}
[16:12:46] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1094}
[16:11:05] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1102}
[16:10:03] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1121}
[16:07:21] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[16:07:21] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S02_TETSUBAN"}
```

## 本日残レース: 33件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 156件 登録 / 123件 締切済
- 通知発射: scan=25 nid / final=28 nid / result=17 nid
- predictions: 19 / うち結果DB記録済: 17
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 3件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S01_NAKAANA1 | 193R | win | 1 | 0.5334 | 4.8 | 2.56 | 200 | scan=3.8 drift=+26.3% | 16:18:58 |
| S00 | 193R | win | 1 | 0.5334 | 4.8 | 2.56 | 300 | scan=4.3 drift=+11.6% | 16:18:55 |
| S01_NAKAANA1 | 0511R | win | 1 | 0.3177 | 3.0 | 0.95 | 200 | scan=- drift=- | 15:45:32 |
| S00 | 0610R | win | 1 | 0.3177 | 4.5 | 1.43 | 300 | scan=- drift=- | 15:36:24 |
| S00 | 119R | win | 1 | 0.4989 | 5.2 | 2.59 | 300 | scan=6.7 drift=-22.4% | 14:19:20 |
| S01_NAKAANA1 | 1811R | win | 1 | 0.5174 | 4.2 | 2.17 | 200 | scan=3.2 drift=+31.2% | 13:47:19 |
| S01_NAKAANA1 | 118R | win | 1 | 0.4111 | 3.5 | 1.44 | 200 | scan=4.1 drift=-14.6% | 13:44:36 |
| S01_NAKAANA1 | 026R | win | 1 | 0.5891 | 3.8 | 2.24 | 200 | scan=3.0 drift=+26.7% | 13:18:31 |
| S00 | 116R | win | 1 | 0.5334 | 5.2 | 2.77 | 300 | scan=4.5 drift=+15.6% | 12:45:32 |
| S00 | 224R | win | 1 | 0.5891 | 5.3 | 3.12 | 300 | scan=- drift=- | 12:15:22 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 82 | +6.4% | -76.2% | +169.2% | 24 | 10 | 58 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 439.9s |
| **Latency** (scan→final max) | 613.7s |
| **Traffic** (notifications 24h) | 82 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 2,400円 used |
| **Saturation** (S01_NAKAANA1) | 2,200円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 418 | 0.4795 | 0.2967 | +0.1828 | 🟡+38% | 0.2486 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 164 | 0.4486 | 0.2134 | 0.2456 | 🔴-0.46 | 0.61 |
| S01_NAKAANA1 | win | 169 | 0.4882 | 0.2899 | 0.2491 | 🔴-0.21 | 0.938 |
| S02_TETSUBAN | win | 85 | 0.5219 | 0.4706 | 0.2535 | 🔴-0.02 | 0.806 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.05-0.10 | 5 | 0.0730 | 0.4000 | 🔴-0.3270 |
| 0.30-0.50 | 162 | 0.4197 | 0.2654 | 🔴+0.1543 |
| 0.50+ | 240 | 0.5425 | 0.3208 | 🔴+0.2217 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 167 | 0.77 |
| win | <5.0 | ✅learned | 292 | 0.766 |
| win | <10.0 | ✅learned | 134 | 0.459 |
| win | <20.0 | ✅learned | 36 | 0.249 |
| win | <50.0 | ⚠️fallback | 8 | 0.1 |
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
_auto-generated by claude_snapshot.py at 2026-10-04T16:20:01.446921+09:00_